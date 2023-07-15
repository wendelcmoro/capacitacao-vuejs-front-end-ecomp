<template>
  <v-container fluid>
    <v-btn flat color="#4c76de" class="white--text" :disabled="addTeamBtn" @click="creating = !creating">
      <v-icon>mdi-plus</v-icon>
    </v-btn>
    <v-dialog v-model="creating" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Adicione um funcionário
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="createIsValid">
            <v-text-field
              v-model="created.nome"
              label="Nome"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Nome é necessário']"
              required
              maxlength="255"
            /><br>
            <v-text-field
              v-model="created.cargo"
              label="Cargo"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Cargo é necessário']"
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
            /><br>
            <v-text-field
              v-model="created.facebook"
              label="Facebook"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Facebook é necessário']"
              required
            /><br>
            <v-text-field
              v-model="created.linkedin"
              label="Linkedin"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Linkedin é necessário']"
              required
            /><br>
            <v-text-field
              v-model="created.twitter"
              label="Twitter"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Twitter é necessário']"
              required
            /><br>
            <v-text-field
              v-model="created.instagram"
              label="Instagram"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Instagram é necessário']"
              required
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
          <v-btn class="white--text" color="#4c76de" :disabled="!createIsValid" @click="createTeam()">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog v-model="editing" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Modifique o funcionário
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="editIsValid">
            <v-text-field
              v-model="edited.nome"
              label="Nome"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Nome é necessário']"
              required
              maxlength="255"
            /><br>
            <v-text-field
              v-model="edited.cargo"
              label="Cargo"
              class="inputUser"
              type="text"
              :rules="[v => !!v || 'Cargo é necessário']"
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
            /><br>
            <v-text-field
              v-model="edited.facebook"
              label="Facebook"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Facebook é necessário']"
              required
            /><br>
            <v-text-field
              v-model="edited.linkedin"
              label="Linkedin"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Linkedin é necessário']"
              required
            /><br>
            <v-text-field
              v-model="edited.twitter"
              label="Twitter"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Twitter é necessário']"
              required
            /><br>
            <v-text-field
              v-model="edited.instagram"
              label="Instagram"
              class="inputUser"
              type="url"
              :rules="[v => !!v || 'Instagram é necessário']"
              required
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
          <v-btn class="white--text" color="#4c76de" :disabled="!editIsValid" @click="upgradeTeam()">
            <v-icon>mdi-pencil</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-row id="teams">
      <v-col
        v-for="team in teams.dados"
        :key="team"
        xs="12"
        sm="6"
        md="6"
        lg="4"
      >
        <v-card>
          <v-list-item three-line>
            <v-list-item-content>
              <v-list-item-title class="TextOnCenter TextTitle">
                {{ team.nome }}
              </v-list-item-title>
              <v-list-item-subtitle class="TextOnCenter">
                {{ team.cargo }}
              </v-list-item-subtitle>
              <p class="TextOnCenter">
                {{ team.descricao }}
              </p>
              <img :src="path + team.imagem.caminho">
              <p class="TextOnCenter">
                <a :href="team.twitter"><v-icon color="blue">mdi-twitter</v-icon></a>
                <a :href="team.facebook"><v-icon color="blue">mdi-facebook</v-icon></a>
                <a :href="team.instagram"><v-icon color="blue">mdi-instagram</v-icon></a>
                <a :href="team.linkedin"><v-icon color="blue">mdi-linkedin</v-icon></a>
              </p>
            </v-list-item-content>
          </v-list-item>
          <v-card-actions>
            <v-btn color="#4c76de" dark @click="upgradeInfo(team.id)">
              <v-icon>mdi-pencil</v-icon>
            </v-btn>
            <v-btn color="#4c76de" dark @click="deleteTeam(team.id)">
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
    const [teamsRes, imagesRes] = await Promise.all([
      $axios.get('/Equipes'),
      $axios.get('/Checaimagem')
    ])
    return {
      teams: teamsRes.data,
      images: imagesRes.data.dados
    }
  },
  data () {
    return {
      message: '',
      addTeamBtn: false,
      createIsValid: true,
      editIsValid: true,
      path: 'http://localhost:8000/imagens/',
      teams: [],
      images: [],
      creating: false,
      created: {
        nome: '',
        cargo: '',
        descricao: '',
        facebook: '',
        twitter: '',
        instagram: '',
        linkedin: '',
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
        this.addTeamBtn = true
      } else {
        this.created.imagem_id = this.images[0].id
        this.created.imagem = this.images[0]
      }
    },
    createTeam () {
      this.$axios.$post('/Novaequipe', this.created)
        .then((res) => {
          this.teams.dados.push(res.dados)
        })
    },
    changeImageCreated (image) {
      this.created.imagem = image
      this.created.imagem_id = image.id
    },
    deleteTeam (idTeam) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir esse funcionário?'
      )
      if (ok) {
        this.$axios.$post('/Eliminaequipe', { id: idTeam })
          .then((res) => {
            this.teams.dados = this.teams.dados.filter(e => e.id !== idTeam)
          })
      }
    },
    upgradeInfo (idTeam) {
      this.edited = this.teams.dados.filter(e => e.id === idTeam)[0]
      this.editing = !this.editing
    },
    changeImageEdited (image) {
      this.edited.imagem = image
      this.edited.imagem_id = image.id
    },
    upgradeTeam () {
      this.$axios.$post('/Atualizaequipe', this.edited)
        .then((res) => {
          this.teams.dados.filter(e => e.id === this.edited.id)[0] = res.dados
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
.TextOnCenter{
  text-align: center;
}
.TextTitle{
  font-size: 1.5rem;
}
</style>
