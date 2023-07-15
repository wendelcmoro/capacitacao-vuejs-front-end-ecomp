<template>
  <v-container class="white--text">
    <v-dialog
      v-model="modalLocal"
      max-width="800px"
      no-click-animation
      persistent
    >
      <!--Inicio modal de editar-->
      <v-card>
        <v-card-title class="headline">
          Mensagem
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap column>
              <v-flex xs12 sm6 md4>
                Nome: {{ editedItem.nome }}
              </v-flex>
            </v-layout>
            <v-layout wrap column>
              <v-flex xs12 sm6 md4>
                Email: {{ editedItem.email }}
              </v-flex>
            </v-layout>
            <v-layout wrap column>
              <v-flex xs12 sm6 md4>
                Assunto: {{ editedItem.assunto }}
              </v-flex>
            </v-layout>
            <v-layout wrap column>
              <v-flex xs12 sm6 md4>
                Mensagem: {{ editedItem.mensagem }}
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="#4c76de" dark @click="close">
            Sair
          </v-btn>
          <v-btn color="#4c76de" dark @click="deletaMensagem(editedItem)">
            Excluir
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-layout class="mt-4">
      <v-flex>
        <v-data-table
          :headers="headers"
          :items="messageInfo"
          :search="search"
          class="elevation-3 bacano"
        >
          <template v-slot:item.action="{ item }">
            <v-btn
              medium
              class="mr-2"
              color="primary"
              @click="viewMessage(item)"
            >
              Vizualizar
            </v-btn>
            <v-icon medium color="error" @click="deletaMensagem(item)">
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
      .get('/Mensagems')
      .then(res => ({ messages: res.data.dados }))
  },
  data () {
    return {
      search: '',
      modalLocal: false,
      editedIndex: -1,
      messages: [],
      headers: [
        { text: 'Nome', align: 'left', value: 'nome' },
        { text: 'Email', align: 'left', value: 'email' },
        { text: 'Assunto', align: 'left', value: 'assunto' },
        { text: '', value: 'action', sortable: false }
      ],
      editedItem: {
        id: 0,
        nome: '',
        email: '',
        assunto: '',
        mensagem: ''
      }
    }
  },

  computed: {
    // funcao MAP JS, serve para pegar elementos específicos da API
    messageInfo () {
      return this.messages.map(c => ({
        id: c.id,
        nome: c.nome,
        email: c.email,
        assunto: c.assunto,
        mensagem: c.mensagem
      }))
    }
  },
  methods: {
    reset () {
      this.$refs.form.reset()
    },
    close () {
      this.modalLocal = false
      setTimeout(() => {
        this.editedItem = Object.assign({}, this.defaultItem)
        this.editedIndex = -1
      }, 300)
    },
    viewMessage (item) {
      this.modalLocal = true
      this.editedIndex = item.id
      this.editedItem = Object.assign({}, item)
    },
    deletaMensagem (item) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir essa mensagem?'
      )
      if (ok) {
        this.$axios
          .post('Deletamensagem', {
            id: item.id
          })
          .then((res) => {
            this.messages = this.messages.filter(e => e.id !== item.id)
          })
          .catch(({ response }) => {
            window.alert('Erro ao deletar mensagem')
          })
        this.close()
      }
    }
  }
}
</script>

<style scoped>
.headline{
  background-color: #2d6760;
  color: white;
}
</style>
