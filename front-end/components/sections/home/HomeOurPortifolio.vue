<template>
  <v-container id="portfolioContainer" fluid>
    <div style="padding-top: 3%;">
      <h1 align="center" id="portifolioTitle">
        Our Portfolio
      </h1>
    </div>
    <div style="margin: 0 auto;">
      <v-tabs
        v-model="tab"
        centered
        color="color"
        slider-color="transparent"
      >
        <v-tab
          v-for="(categoria,i) in categorias"
          :key="(categoria,i)"
        >
          {{ categoria.nome }}
          <!-- <v-btn color="white" dark>{{ categoria.nome }}</v-btn> -->
        </v-tab>
      </v-tabs>
    </div>
    <v-tabs-items v-model="tab">
      <v-tab-item
        v-for="(x,i) in categorias"
        :key="(x,i)"
      >
        <v-container fluid>
          <v-row justify="center">
            <v-col
              v-for="portfolio in filterCategories(i, x.nome)"
              :key="portfolio"
              cols="12"
              sm="6"
              md="6"
              lg="4"
            >
              <template>
                <a :href="portfolio.link"><img :src="path + portfolio.imagem.caminho" style="width: 100%; height: 100%;"></a>
              </template>
            </v-col>
          </v-row>
        </v-container>
      </v-tab-item>
    </v-tabs-items>
  </v-container>
</template>

<script>
export default {
  name: 'HomeOurPortifolio',
  color: 'purple',
  props: {
    portfolios: Array,
    categorias: Array
  },
  data () {
    return {
      tab: null,
      path: 'http://localhost:8000/imagens/'
    }
  },
  mounted () {
    this.categorias.unshift({ id: 0, nome: 'ALL' })
  },
  methods: {
    filterCategories (i, category) {
      if (i === 0) {
        return this.portfolios.dados
      } else {
        return this.portfolios.dados.filter(e => e.categorias[0].nome === category)
      }
    }
  }
}
</script>

<style scopedb>
div.v-select-list {
    background-color:#00857A;
}
#portifolioTitle {
  font-family: "Lato";
  color:  #787474;
  font-weight: 300;
  font-size: 2.5rem;
}
#portfolioContainer {
  background-color: white;
  padding: 3.5rem 1rem;
  text-align: center;
}
@media (min-width: 600px) {
  #portfolioContainer{
    padding: 3.5rem 2rem;
  }
}
@media (min-width: 960px) {
  #portfolioContainer{
    padding: 3.5rem 8rem;
  }
}
</style>
