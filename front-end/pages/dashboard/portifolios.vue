<template>
  <v-container class="white--text">
    <v-layout>
      <v-flex>
        <span class="font-weight-thin display-2">PORTFÓLIO</span>
      </v-flex>
    </v-layout>
    <v-divider color="grey" />
    <v-card-title>
      <v-btn
        class="mt-10"
        color="#4c76de"
        dark
        @click.stop="modalLocal = !modalLocal"
      >
        <v-icon>mdi-plus</v-icon>
      </v-btn>
      <v-spacer />
      <!-- <v-text-field
        v-model="search"
        append-icon="mdi-magnify"
        label="Pesquisar"
        single-line
        hide-details
      /> -->
    </v-card-title>
    <v-dialog
      v-model="modalLocal"
      max-width="800px"
      no-click-animation
      persistent
    >
      <!--Inicio modal de editar-->
      <v-card>
        <v-card-title class="headline">
          {{ formTitle() }}
        </v-card-title>
        <v-card-text>
          <v-container grid-list-md>
            <v-layout wrap column>
              <v-flex xs12 sm6 md4>
                <v-form ref="form" v-model="validation">
                  <v-select
                    v-model="editedItem.categoria_id[0]"
                    :items="categoriasInfo"
                    item-text="nome"
                    item-value="id"
                    label="Categoria"
                  />
                  <v-text-field
                    v-model="editedItem.link"
                    :rules="[(v) => !!v || 'Campo Obrigatório']"
                    label="Link"
                  />
                  <v-select
                    v-model="editedItem.imagem_id"
                    :items="imagensInfo"
                    item-text="nome"
                    item-value="id"
                    label="Imagem"
                  />
                </v-form>
              </v-flex>
            </v-layout>
          </v-container>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="#4c76de" dark @click="close">
            Cancelar
          </v-btn>
          <v-btn color="#4c76de" dark @click="reset">
            Reiniciar
          </v-btn>
          <v-btn color="#4c76de" dark @click="onSubmit">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
    <v-row>
      <v-col
        v-for="portfolio in portfolios.dados"
        :key="portfolio"
        xs="12"
        sm="6"
        md="6"
        lg="4"
      >
        <v-card>
          <v-list-item three-line>
            <v-list-item-content>
              <v-list-item-title>{{ portfolio.link }}</v-list-item-title>
              <v-list-item-subtitle>{{ portfolio.categorias[0].nome }}</v-list-item-subtitle>
              <img :href="portfolio.link" :src="path + portfolio.imagem.caminho">
            </v-list-item-content>
          </v-list-item>
          <v-card-actions>
            <v-btn color="#4c76de" dark>
              <v-icon @click="dialogEdit(portfolio)">
                mdi-pencil
              </v-icon>
            </v-btn>
            <v-btn color="#4c76de" dark>
              <v-icon @click="deletaPortfolio(portfolio)">
                mdi-delete
              </v-icon>
            </v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  layout: 'dashboard',
  async asyncData ({ $axios }) {
    const [portfoliosRes, imagensRes, categoriasRes] = await Promise.all([
      $axios.get('/Portfolios'),
      $axios.get('/Checaimagem'),
      $axios.get('/Checacategoria')
    ])
    return {
      portfolios: portfoliosRes.data,
      imagens: imagensRes.data.dados,
      categories: categoriasRes.data.dados
    }
  },
  data () {
    return {
      search: '',
      modalLocal: false,
      validation: true,
      editedIndex: -1,
      path: 'http://localhost:8000/imagens/',
      headers: [
        { text: 'Categoria', value: 'categoria_id' },
        { text: 'Link', align: 'left', value: 'link', sortable: false },
        { text: 'Imagens', value: 'imagem_id', sortable: false },
        { text: '', value: 'action', sortable: false }
      ],
      portfolios: [],
      imagens: [],
      categories: [],
      editedItem: {
        id: 0,
        categoria_id: [],
        link: '',
        imagem_id: ''
      },
      defaultItem: {
        id: 0,
        categoria_id: [],
        link: '',
        imagem_id: ''
      }
    }
  },

  computed: {
    // funcao MAP JS, serve para pegar elementos específicos da API
    portfoliosInfo () {
      return this.portfolios.map(c => ({
        id: c.id,
        categoria_id: c.categoria_id,
        link: c.link,
        imagem_id: c.imagem_id
      }))
    },
    imagensInfo () {
      return this.imagens.map(c => ({
        id: c.id,
        nome: c.titulo,
        descricao: c.descricao
      }))
    },
    categoriasInfo () {
      return this.categories.map(c => ({
        id: c.id,
        nome: c.nome
      }))
    },

    onSignup () {
      return this.editedIndex === -1
    }
  },
  methods: {
    compare (item) {
      const x = item.imagem_id
      return this.imagens[x - 1].nome
    },
    nomeCategoria (item) {
      const x = item.categoria_id
      return this.categorias[x - 1].categoria
    },
    formTitle () {
      return this.editedIndex === -1 ? 'NOVO PORTFÓLIO' : 'EDITAR PORTFÓLIO'
    },
    onSubmit () {
      if (!this.validation) {
        this.$refs.form.validate()
        return
      }
      if (this.onSignup) {
        this.novoPortfolio()
      } else {
        this.atualizaPortfolio()
      }
      this.close()
    },
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
    novoPortfolio () {
      //  váriavel com todos os dados dos serviços
      const PortfolioData = {
        id: this.editedItem.id,
        imagem_id: this.editedItem.imagem_id,
        categoria_id: this.editedItem.categoria_id,
        link: this.editedItem.link
      }
      this.$axios
        .$post('Novoportfolio', PortfolioData)
        .then((res) => {
          this.portfolios.push(res.dados)
        })
        .catch(({ response }) => {
          const { mensagem, errosSecundarios: erros } = response.data
          const listaErros = erros ? `\n ${Object.values(erros).join('\n')}` : ''
          window.alert(`${mensagem}${listaErros}`)
        })
        // .catch(({ response }) => {
        //   window.alert('Campo Inválido')
        // })
      window.location.reload()
    },
    atualizaPortfolio () {
      const editablePortofolioData = {
        id: this.editedItem.id,
        imagem_id: this.editedItem.imagem_id,
        categoria_id: this.editedItem.categoria_id,
        link: this.editedItem.link
      }
      this.$axios
        .$post('Atualizaportfolio', editablePortofolioData)
        .then((res) => {
          this.portfolios = this.portfolios.map((e) => {
            if (e.id === this.editedItem.id) {
              return Object.assign(e, editablePortofolioData)
            }
            return e
          })
        })
        .catch(({ response }) => {
          const { mensagem, errosSecundarios: erros } = response.data
          const listaErros = erros ? `\n ${Object.values(erros).join('\n')}` : ''
          window.alert(`${mensagem}${listaErros}`)
        })
        // .catch(({ response }) => {
        //   window.alert('Erro ao editar Portfólio')
        // })
      window.location.reload()
    },
    dialogEdit (item) {
      this.modalLocal = true
      this.editedIndex = item.id
      // this.editedItem = Object.assign({}, item)
      this.editedItem.id = item.id
      this.editedItem.categoria = item.categoria_id
      this.editedItem.link = item.link
      this.editedItem.imagem_id = item.imagem_id
    },
    deletaPortfolio (item) {
      const ok = window.confirm(
        'Você tem certeza de que deseja excluir esse portfólio?'
      )
      if (ok) {
        this.$axios
          .post('Deletaportfolio', {
            id: item.id
          })
          .then((res) => {
            this.portfolios = this.portfolios.filter(e => e.id !== item.id)
          })
          .catch(({ response }) => {
            window.alert('Erro ao deletar portfólio')
          })
      }
      window.location.reload()
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
