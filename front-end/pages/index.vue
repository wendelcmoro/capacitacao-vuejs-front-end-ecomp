<template>
  <v-content>
    <v-container id="firstImage" fluid>
      <HomeWelcome />
      <homeAboutUs />
      <Services :services="services" />
      <v-container id="secondImage" class="ma-0" fluid>
        <HomeCalltoAction />
        <HomeOurPortifolio :portfolios="portfolios" :categorias="categorias" />
        <HomeFrequentlyQuestions />
        <OurTeam :teams="teams" />
        <HomeContactUs :contacts="contacts" />
        <Map />
        <Footer />
      </v-container>
    </v-container>
  </v-content>
</template>

<script>
import HomeWelcome from '../components/sections/home/Welcome.vue'
import HomeAboutUs from '../components/sections/home/HomeAboutUs.vue'
import HomeCalltoAction from '../components/sections/home/HomeCalltoAction.vue'
import HomeFrequentlyQuestions from '../components/sections/home/HomeFrequentlyQuestions.vue'
import HomeContactUs from '../components/sections/home/HomeContactUs.vue'
import HomeOurPortifolio from '../components/sections/home/HomeOurPortifolio.vue'
import Services from '~~/components/sections/home/Services.vue'
import OurTeam from '~~/components/sections/home/OurTeam.vue'
import Map from '~~/components/sections/home/Map.vue'
import Footer from '~~/components/sections/home/Footer.vue'

export default {
  components: {
    HomeWelcome,
    HomeAboutUs,
    HomeCalltoAction,
    HomeOurPortifolio,
    HomeFrequentlyQuestions,
    HomeContactUs,
    Services,
    OurTeam,
    Map,
    Footer
  },
  async asyncData ({ $axios }) {
    const [servicesRes, portfoliosRes, categoriasRes, teamsRes, contactsRes] = await Promise.all([
      $axios.get('/ListaServico'),
      $axios.get('/Portfolios'),
      $axios.get('/Checacategoria'),
      $axios.get('/Equipes'),
      $axios.get('/Checacontato')
    ])
    return {
      services: servicesRes.data,
      portfolios: portfoliosRes.data,
      categorias: categoriasRes.data.dados,
      teams: teamsRes.data,
      contacts: contactsRes.data.dados
    }
  },
  head () {
    return {
      title: 'Amoeba',
      meta: [
        {
          hid: 'description',
          name: 'description',
          content: 'Site da Amoeba'
        }
      ]
    }
  },
  layout: 'default'
}
</script>

<style>
#firstImage {
  background: lightblue url("../static/imagens/hero-background.jpg") fixed;
  padding: 0;
  margin: 0;
  border: 0;
  height: 1500px;
}
#secondImage {
  background: lightblue url("../static/imagens/call-to-action-bg.jpg") fixed;
  padding: 0;
  margin: 0;
  border: 0;
  background-size: 100%;
  height: 99%;
}
</style>
