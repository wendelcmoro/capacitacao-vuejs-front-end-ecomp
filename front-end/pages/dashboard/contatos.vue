<template>
  <v-container fluid>
    <v-layout>
      <v-flex 3>
        <v-btn flat color="#4c76de" class="white--text" @click="openContactForm()">
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </v-flex>
      <v-flex 9>
        <v-text-field
          id="teste"
          v-model="search"
          append-icon="mdi-magnify"
          label="Pesquisar"
          single-line
          hide-details
        />
      </v-flex>
    </v-layout>
    <v-dialog v-model="addContact" max-width="400">
      <v-card>
        <v-card-title class="headline">
          {{ formTitle() }}
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form>
            <v-text-field
              v-model="contactData.endereco"
              label="Endereço"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Endereço é necessário']"
              required
              maxlength="255"
            /><br>
            <v-text-field
              v-model="contactData.email"
              label="Email"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Email é necessário']"
              required
              maxlength="255"
            /><br>
            <v-text-field
              v-model="contactData.telefone"
              label="Telefone"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Telefone é necessário']"
              required
              maxlength="500"
            /><br>
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn class="white--text" color="#4c76de" @click="onSubmit()">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
          <v-btn dark color="#4c76de" @click="closeAddContact()">
            Cancelar
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-layout class="mt-4">
      <v-flex>
        <v-data-table
          :search="search"
          :headers="headers"
          :items="contactsList"
          class="elevation-3"
        >
          <template v-slot:item.action="{ item }">
            <v-icon medium class="mr-2" @click="dialogEdit(item)">
              mdi-pencil
            </v-icon>
            <v-icon medium class="mr-2" @click="destroyContact(item)">
              mdi-delete
            </v-icon>
          </template>
        </v-data-table>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
export default {
  layout: 'dashboard',
  asyncData (context) {
    return context.app.$axios
      .get('/Checacontato')
      .then(res => ({ contacts: res.data.dados }))
  },
  data () {
    return {
      search: '',
      message: '',
      addServiceBtn: false,
      createIsValid: true,
      editIsValid: true,
      addContact: false,
      contacts: [],
      editedIndex: -1,
      teste: '',
      contactData: {
        id: 0,
        endereco: '',
        email: '',
        telefone: ''
      },
      headers: [
        { text: 'Endereço', align: 'left', sortable: true, value: 'endereco' },
        { text: 'Email', sortable: true, value: 'email' },
        { text: 'Telefone', value: 'telefone', sortable: true },
        { text: '', value: 'action', sortable: false }
      ],
      editing: false
    }
  },
  computed: {
    contactsList () {
      return this.contacts.map(z => ({
        id: z.id,
        endereco: z.endereco,
        email: z.email,
        telefone: z.telefone
      }))
    }
  },
  methods: {
    openContactForm () {
      this.addContact = true
      this.contactData.endereco = ''
      this.contactData.email = ''
      this.contactData.telefone = ''
      this.editedIndex = -1
    },
    formTitle () {
      return this.editedIndex === -1 ? 'Adicionar Contato' : 'Editar Contato'
    },
    closeAddContact () {
      this.addContact = false
    },
    onSubmit () {
      if (this.editedIndex === -1) {
        this.createContact()
      } else {
        this.updateContact()
      }
      this.closeAddContact()
    },
    createContact () {
      this.$axios
        .$post('/Novocontato', this.contactData)
        .then((res) => {
          this.contacts.push(res.dados)
        })
        .catch(({ response }) => {
          const { mensagem, errosSecundarios: erros } = response.data
          const listaErros = erros ? `\n ${Object.values(erros).join('\n')}` : ''
          window.alert(`${mensagem}${listaErros}`)
        })
    },
    dialogEdit (item) {
      this.addContact = true
      this.editedIndex = item.id
      this.contactData = Object.assign({}, item)
    },
    updateContact () {
      const editableContactData = {
        id: this.contactData.id,
        endereco: this.contactData.endereco,
        email: this.contactData.email,
        telefone: this.contactData.telefone
      }
      this.$axios
        .$post('/Atualizacontato', editableContactData)
        .then((res) => {
          this.contacts = this.contacts.map((e) => {
            if (e.id === this.contactData.id) {
              return Object.assign(e, editableContactData)
            }
            return e
          })
        })
        .catch(({ response }) => {
          const { mensagem, errosSecundarios: erros } = response.data
          const listaErros = erros ? `\n ${Object.values(erros).join('\n')}` : ''
          window.alert(`${mensagem}${listaErros}`)
        })
    },
    destroyContact (item) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir esse portfólio?'
      )
      if (ok) {
        this.$axios
          .$post('/Deletacontato', { id: item.id })
          .then((res) => {
            this.contacts = this.contacts.filter(e => e.id !== item.id)
          })
          .catch(({ response }) => {
            window.alert('Erro ao deletar Contato')
          })
      }
    }
  }
}
</script>
<style>
.headline{
  background-color: #2d6760;
  color: white;
}
#inputBox{
  padding: 1rem 0.5rem;
}
.inputUser{
  font-size: 1rem;
  padding: 0.2rem;
  width: 100%;
}
#teste{
  width: 100%;
  padding-right: 0rem;
}
#searchContact {
  margin-top: 3%;
  margin-left: 5%;
}
@media only screen and (max-width: 800px) {
  #searchContact {
    margin-top: 8%;
    margin-left: 5%;
  }
}
</style>
