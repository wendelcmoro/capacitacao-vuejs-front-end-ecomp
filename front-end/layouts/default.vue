<template>
  <v-app>
    <div class="Pagina">
      <v-app-bar
        dense
        fixed
        flat
        height="80"
        :color="navbarColor"
      >
        <v-toolbar-title id="titulonav" @click="$vuetify.goTo(0,0,2)">
          Amoeba
        </v-toolbar-title>

        <div id="botao">
          <v-btn text dark depressed small @click="$vuetify.goTo('#welcomeBackground',0,2)">
            Home
          </v-btn>
          <v-btn text dark depressed small @click="$vuetify.goTo('#aboutContainer',0,2)">
            About Us
          </v-btn>
          <v-btn text dark depressed small @click="$vuetify.goTo('#servicesBackground',0,2)">
            Services
          </v-btn>
          <v-btn text dark depressed small @click="$vuetify.goTo('#portfolioContainer',0,2)">
            Portifolio
          </v-btn>
          <v-btn text dark depressed small @click="$vuetify.goTo('#teamsBackground',0,2)">
            Team
          </v-btn>
          <v-menu offset-y>
            <template v-slot:activator="{ on }">
              <v-btn text dark depressed small v-on="on">
                Drop Down
                <v-icon left>
                  mdi-chevron-down
                </v-icon>
              </v-btn>
            </template>

            <v-list>
              <v-list-item v-for="link in links" :key="link.text">
                <v-list-item-title>{{ link.text }}</v-list-item-title>
              </v-list-item>
            </v-list>
          </v-menu>
          <v-btn text dark depressed small @click="$vuetify.goTo('#contactBackground',0,2)">
            Contact Us
          </v-btn>
        </div>

        <div id="menu">
          <v-app-bar-nav-icon dark depressed small @click.stop="drawer = !drawer" />
        </div>
      </v-app-bar>
    </div>
    <v-navigation-drawer
      v-model="drawer"
      temporary
      right
      sm-and-down
      app
      width="180px"
      height="340px"
      color="#2d6760"
    >
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#welcomeBackground',0,2)">
          Home
        </v-btn>
      </v-list-item>
      <v-divider />
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#aboutContainer',0,2)">
          About Us
        </v-btn>
      </v-list-item>
      <v-divider />
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#servicesBackground',0,2)">
          Services
        </v-btn>
      </v-list-item>
      <v-divider />
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#portfolioContainer',0,2)">
          Portifolio
        </v-btn>
      </v-list-item>
      <v-divider />
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#teamsBackground',0,2)">
          Team
        </v-btn>
      </v-list-item>
      <v-divider />
      <v-menu offset-x left top>
        <template v-slot:activator="{ on }">
          <v-list-item dark>
            <v-btn color="#2d6760" dark depressed small v-on="on">
              <v-icon left>
                mdi-chevron-down
              </v-icon>
              Drop Down
            </v-btn>
          </v-list-item>
        </template>

        <v-list>
          <v-list-item v-for="link in links" :key="link.text">
            <v-list-item-title>{{ link.text }}</v-list-item-title>
          </v-list-item>
        </v-list>
      </v-menu>
      <v-divider />
      <v-list-item dark>
        <v-btn color="#2d6760" dark depressed small @click="$vuetify.goTo('#contactBackground',0,2)">
          Contact Us
        </v-btn>
      </v-list-item>
    </v-navigation-drawer>
    <!-- Conteúdo da página -->
    <v-content @scroll="onScroll()">
      <nuxt />
    </v-content>
    <!-- <v-footer
      :padless="padless"
      app
      color="#2d6760"
      fixed
      dark
      height="100"
    >
    </v-footer> -->
  </v-app>
</template>

<script>
import _ from 'lodash'

export default {
  data: () => ({
    navbarColor: '#2d6760',
    scrolled: false,
    links: [
      { text: 'Click Me' },
      { text: 'Click Me' },
      { text: 'Click Me' },
      { text: 'Click Me 2' }
    ],
    drawer: null,
    return: {
      testando: {
        round: true,
        depressed: true,
        color: 'transparent',
        class: 'link-navbar white--text'
      }
    }
  }),
  mounted () {
    window.addEventListener('scroll', this.onScroll)
  },
  beforeDestroy () {
    window.removeEventListener('scroll', this.onScroll)
  },
  methods: {
    onScroll: _.throttle(function handle () {
      if (window.scrollY > 0 && this.navbarColor === 'rgba(0,0,0,0.6)') {
        this.navbarColor = '#2d6760'
      } else if (window.scrollY === 0 && this.navbarColor !== 'rgba(0,0,0,0.6)') {
        this.navbarColor = 'rgba(0,0,0,0.6)'
      }
    }, 100)
  },
  scrollY () {
    window.scrollTo(100, 100)
  }
}

</script>

<style>
#menu {
  display: none;
}
#titulonav {
  color: white;
  font-size: 1.8rem;
  font-weight: bold;
  padding-left: 450px;
}
#titulonav:hover {
  cursor: pointer;
}
#botao{
  font-size: 1pt;
  padding-right:0px;
  padding-left: 450px;
  font-family: "sans-serif";
}
.linksnav:not(.fora) {
  margin-right: 2rem;
}
.linksnav span {
  font-size: 0.9rem;
  transition: 0.3s;
  color: #b8cab9;
}
.linksnav:hover span {
  color: #98d1ca;
}
.Pagina{
  font-family: "Roboto";
  font-weight: normal;
}
@media only screen and (max-width: 1717px) {
  #titulonav {
    color: white;
    font-size: 1.8rem;
    font-weight: 500;
    padding-left: 250px;
  }
  #botao {
    font-size: 1pt;
    padding-left:350px;
  }
}
@media only screen and (max-width: 1510px) {
  #titulonav {
    color: white;
    font-size: 1.8rem;
    font-weight: 500;
    padding-left: 200px;
  }
  #botao {
    font-size: 1pt;
    padding-left:200px;
  }
}

@media only screen and (max-width: 1300px) {
  #botao {
    font-size: 1pt;
    margin-left:auto;
    margin-right:0;
  }
  #titulonav {
    color: white;
    font-size: 1.8rem;
    font-weight: 500;
    padding: 10px;
  }
}
@media only screen and (max-width: 1108px) {
  #botao {
    display: none;
    font-size: 1pt;
    margin-left:auto;
    margin-right:0;
  }
  #menu {
    display: inline;
    margin-left:auto;
    margin-right: 0;
  }
  #titulonav {
    color: white;
    font-size: 1.8rem;
    font-weight: 500;
    padding: 10px;
  }
}
</style>
