<template>
  <v-container fluid>
    <v-btn flat color="#4c76de" dark @click="creating = !creating">
      <v-icon>mdi-image-plus</v-icon>
    </v-btn>
    <v-dialog v-model="creating" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Adicione uma imagem
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="addIsValid">
            <v-text-field
              v-model="created.titulo"
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
            <v-file-input
              v-model="picture"
              label="Imagem"
              type="file"
              :rules="[v => !!v || 'Imagem é necessário']"
              required
            />
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn class="white--text" color="#4c76de" :disabled="!addIsValid" @click="addImage()">
            <v-icon>mdi-image-plus</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-dialog v-model="editing" max-width="400">
      <v-card>
        <v-card-title class="headline">
          Modifique a imagem
        </v-card-title>
        <v-card-text id="inputBox">
          <v-form v-model="editIsValid">
            <v-text-field
              v-model="edited.titulo"
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
            <v-file-input
              v-model="picture"
              label="Imagem"
              type="file"
              :rules="[v => !!v || 'Imagem é necessário']"
              required
            />
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-btn class="white--text" color="#4c76de" :disabled="!editIsValid" @click="upgradeImage()">
            <v-icon>mdi-image-edit</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-row id="images">
      <v-col
        v-for="image in images.dados"
        :key="image"
        xs="12"
        sm="6"
        md="6"
        lg="4"
      >
        <v-card>
          <v-list-item three-line>
            <v-list-item-content>
              <v-list-item-title>{{ image.titulo }}</v-list-item-title>
              <v-list-item-subtitle>{{ image.descricao }}</v-list-item-subtitle>
              <img :src="path + image.caminho">
            </v-list-item-content>
          </v-list-item>
          <v-card-actions>
            <v-btn color="#4c76de" dark @click="upgradeInfo(image.id)">
              <v-icon>mdi-image-edit</v-icon>
            </v-btn>
            <v-btn color="#4c76de" dark @click="deleteImage(image.id)">
              <v-icon>mdi-image-minus</v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
function getFormData (object) {
  const formData = new FormData()
  Object.keys(object).forEach(key => formData.append(key, object[key]))
  return formData
}
export default {
  layout: 'dashboard',
  asyncData (context) {
    return context.app.$axios
      .get('/Checaimagem')
      .then(res => ({ images: res.data }))
  },
  data () {
    return {
      addIsValid: true,
      editIsValid: true,
      path: 'http://localhost:8000/imagens/',
      images: [],
      picture: '',
      creating: false,
      created: {
        titulo: 'Titulo',
        descricao: 'Descrição',
        imagem: ''
      },
      editing: false,
      edited: {}
    }
  },
  methods: {
    addImage () {
      const request = getFormData(this.created)
      request.append('imagem', this.picture)
      this.$axios.$post('/novaImagem', request, {
        headers: { 'Content-Type': 'multipart/form-data' }
      })
        .then((res) => {
          this.images.dados.push(res.dados)
        })
    },
    deleteImage (idImage) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir essa imagem?'
      )
      if (ok) {
        this.$axios.$post('/Deletaimagem', { id: idImage })
          .then((res) => {
            this.images.dados = this.images.dados.filter(e => e.id !== idImage)
          })
      }
    },
    upgradeInfo (idImage) {
      this.edited = this.images.dados.filter(e => e.id === idImage)[0]
      this.editing = !this.editing
    },
    upgradeImage () {
      const request = getFormData(this.edited)
      request.set('imagem', this.picture)
      this.$axios.$post('/Atualizaimagem', request, {
        headers: { 'Content-Type': 'multipart/form-data' }
      })
        .then((res) => {
          console.log(this.images.dados.filter(e => e.id === this.edited.id)[0])
          console.log(res.dados)
          this.images.dados.filter(e => e.id === this.edited.id)[0].caminho = res.dados.caminho
          console.log(this.images.dados.filter(e => e.id === this.edited.id)[0])
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
