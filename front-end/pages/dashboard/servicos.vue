inputBox<template>
  <v-container fluid>
    <v-btn flat color="#4c76de" class="white--text" :disabled="addServiceBtn" @click="creating = !creating">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="creating" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Adicione um serviço
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="createIsValid">
            <v-text-field
              v-model="created.servico"
              label="Titulo"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Titulo é necessário']"
              required
              maxlength="255"
            /><br>
            <v-textarea
              v-model="created.descricao"
              label="Descrição"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Descrição é necessário']"
              required
              maxlength="500"
            /><br>
            <v-expansion-panels>
              <v-expansion-panel>
                <v-expansion-panel-header>Imagem selecionada:</v-expansion-panel-header>
                <v-expansion-panel-content>
                  <v-card>
                    <v-list-item three-line>
                      <v-list-item-content>
                        <img :src="path + created.imagem.caminho">
                      </v-list-item-content>
                    </v-list-item>
                  </v-card>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </v-form>
          <v-expansion-panels class="mt-3">
            <v-expansion-panel>
              <v-expansion-panel-header>Selecione outra imagem:</v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-list-item-group color="#2d6760">
                  <v-row no-gutters>
                    <v-col v-for="image in images" :key="image" xs="12" md="6">
                      <v-list-item three-line @click="changeImageCreated(image)">
                        <v-list-item-content>
                          <v-list-item-title>{{ image.titulo }}</v-list-item-title>
                          <v-list-item-subtitle>{{ image.descricao }}</v-list-item-subtitle>
                          <img :src="path + image.caminho">
                        </v-list-item-content>
                      </v-list-item>
                    </v-col>
                  </v-row>
                </v-list-item-group>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-card-text>
        <v-card-actions>
          <v-btn class="white--text" color="#4c76de" :disabled="!createIsValid" @click="createService()">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog v-model="editing" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Modifique o serviço
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="editIsValid">
            <v-text-field
              v-model="edited.servico"
              label="Titulo"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Titulo é necessário']"
              required
              maxlength="255"
            /><br>
            <v-textarea
              v-model="edited.descricao"
              label="Descrição"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Descrição é necessário']"
              required
              maxlength="500"
            /><br>
            <v-expansion-panels>
              <v-expansion-panel>
                <v-expansion-panel-header>Imagem selecionada:</v-expansion-panel-header>
                <v-expansion-panel-content>
                  <v-card>
                    <v-list-item three-line>
                      <v-list-item-content>
                        <img :src="path + edited.imagem.caminho">
                      </v-list-item-content>
                    </v-list-item>
                  </v-card>
                </v-expansion-panel-content>
              </v-expansion-panel>
            </v-expansion-panels>
          </v-form>
          <v-expansion-panels class="mt-3">
            <v-expansion-panel>
              <v-expansion-panel-header>Selecione outra imagem:</v-expansion-panel-header>
              <v-expansion-panel-content>
                <v-list-item-group color="#2d6760">
                  <v-row no-gutters>
                    <v-col v-for="image in images" :key="image" xs="12" md="6">
                      <v-list-item three-line @click="changeImageEdited(image)">
                        <v-list-item-content>
                          <v-list-item-title>{{ image.titulo }}</v-list-item-title>
                          <v-list-item-subtitle>{{ image.descricao }}</v-list-item-subtitle>
                          <img :src="path + image.caminho">
                        </v-list-item-content>
                      </v-list-item>
                    </v-col>
                  </v-row>
                </v-list-item-group>
              </v-expansion-panel-content>
            </v-expansion-panel>
          </v-expansion-panels>
        </v-card-text>
        <v-card-actions>
          <v-btn class="white--text" color="#4c76de" :disabled="!editIsValid" @click="upgradeService()">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-row id="services">
      <v-col
        v-for="service in services.dados"
        :key="service"
        xs="12"
        sm="6"
        md="6"
        lg="4"
      >
        <v-card>
          <v-list-item three-line>
            <v-list-item-content>
              <v-list-item-title>{{ service.servico }}</v-list-item-title>
              <v-list-item-subtitle>{{ service.descricao }}</v-list-item-subtitle>
              <img :src="path + service.imagem.caminho">
            </v-list-item-content>
          </v-list-item>
          <v-card-actions>
            <v-btn color="#4c76de" dark @click="upgradeInfo(service.id)">
              <v-icon>mdi-pencil</v-icon>
            </v-btn>
            <v-btn color="#4c76de" dark @click="deleteService(service.id)">
              <v-icon>mdi-delete</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
    {{ message }}
  </v-container>
</template>

<script>
export default {
  layout: 'dashboard',
  async asyncData ({ $axios }) {
    const [servicesRes, imagesRes] = await Promise.all([
      $axios.get('/ListaServico'),
      $axios.get('/Checaimagem')
    ])
    return {
      services: servicesRes.data,
      images: imagesRes.data.dados
    }
  },
  data () {
    return {
      message: '',
      addServiceBtn: false,
      createIsValid: true,
      editIsValid: true,
      path: 'http://localhost:8000/imagens/',
      services: [],
      images: [],
      creating: false,
      created: {
        servico: '',
        descricao: '',
        imagem_id: '',
        imagem: {}
      },
      editing: false,
      edited: {
        imagem: {}
      }
    }
  },
  mounted () {
    this.randomImage()
  },
  methods: {
    randomImage () {
      if (this.images[0] == null) {
        this.message = 'Adicione uma imagem antes'
        this.addServiceBtn = true
      } else {
        this.created.imagem_id = this.images[0].id
        this.created.imagem = this.images[0]
      }
    },
    createService () {
      this.$axios.$post('/CriaServico', this.created)
        .then((res) => {
          this.services.dados.push(res.dados)
        })
    },
    changeImageCreated (image) {
      this.created.imagem = image
      this.created.imagem_id = image.id
    },
    deleteService (idService) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir esse serviço?'
      )
      if (ok) {
        this.$axios.$post('/DeletaServico', { id: idService })
          .then((res) => {
            this.services.dados = this.services.dados.filter(e => e.id !== idService)
          })
      }
    },
    upgradeInfo (idService) {
      this.edited = this.services.dados.filter(e => e.id === idService)[0]
      this.editing = !this.editing
    },
    changeImageEdited (image) {
      this.edited.imagem = image
      this.edited.imagem_id = image.id
    },
    upgradeService () {
      this.$axios.$post('/AtualizarServico', this.edited)
        .then((res) => {
          this.services.dados.filter(e => e.id === this.edited.id)[0] = res.dados
          this.editing = !this.editing
        })
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
</style>
