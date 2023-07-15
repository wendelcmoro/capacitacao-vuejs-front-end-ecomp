<template>
  <v-container id="teamsBackground" fluid>
    <div class="teams-header">
      <h1 class="teams-title">
        Our Team
      </h1>
      <p class="teams-text">
        Magnam dolores commodi suscipit. Necessitatibus eius consequatur ex aliquid fuga eum quidem. Sit sint consectetur velit. Quisquam quos quisquam cupiditate. Et nemo qui impedit suscipit alias ea. Quia fugiat sit in iste officiis commodi quidem hic quas.
      </p>
    </div>
    <v-row id="teams" justify="center">
      <v-col
        v-for="team in teams.dados"
        :key="team"
        cols="12"
        sm="6"
        md="6"
        lg="4"
      >
        <v-card>
          <v-list-item three-line>
            <v-list-item-content>
              <div class="portrait">
                <div class="people">
                  <img :src="path + team.imagem.caminho" class="people-image">
                </div>
              </div>
              <v-list-item-title class="people-name">
                {{ team.nome }}
              </v-list-item-title>
              <v-list-item-subtitle class="people-position">
                {{ team.cargo }}
              </v-list-item-subtitle>
              <p class="people-description">
                {{ team.descricao }}
              </p>
              <p class="people-accounts">
                <v-hover
                  v-slot:default="{ hover }"
                  open-delay="100"
                >
                  <a :href="team.twitter">
                    <v-icon :color="hover ? '#43aea0' : '#92cac3'">mdi-twitter</v-icon>
                  </a>
                </v-hover>
                <v-hover
                  v-slot:default="{ hover }"
                  open-delay="100"
                >
                  <a :href="team.facebook">
                    <v-icon :color="hover ? '#43aea0' : '#92cac3'">mdi-facebook</v-icon>
                  </a>
                </v-hover>
                <v-hover
                  v-slot:default="{ hover }"
                  open-delay="100"
                >
                  <a :href="team.instagram">
                    <v-icon :color="hover ? '#43aea0' : '#92cac3'">mdi-instagram</v-icon>
                  </a>
                </v-hover>
                <v-hover
                  v-slot:default="{ hover }"
                  open-delay="100"
                >
                  <a :href="team.linkedin">
                    <v-icon :color="hover ? '#43aea0' : '#92cac3'">mdi-linkedin</v-icon>
                  </a>
                </v-hover>
              </p>
            </v-list-item-content>
          </v-list-item>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
export default {
  name: 'OurTeam',
  props: {
    teams: Array
  },
  data () {
    return {
      path: 'http://localhost:8000/imagens/'
    }
  },
  methods: {

  }
}
</script>

<style>
/* */
#teamsBackground{
  background-color: white;
  padding: 3.5rem 1rem;
  text-align: center;
}
@media (min-width: 600px) {
  #teamsBackground{
    padding: 3.5rem 2rem;
  }
}
@media (min-width: 960px) {
  #teamsBackground{
    padding: 3.5rem 8rem;
  }
}
.teams-header{
  color: #555;
}
.teams-title{
  font-family: "Lato";
  font-weight: 300;
  margin-bottom: 1rem;
  font-size: 2.5rem;
}
.teams-text{
  color: #777;
  line-height: 1.5;
  font-family: sans-serif;
}
.portrait{
  padding: 1.5rem 0;
}
.people{
  position: relative;
  width: 190px;
  height: 190px;
  overflow: hidden;
  margin: 0 auto;
  border-radius: 50%;
}
.people-image{
  position: absolute;
  left: 50%;
  top: 50%;
  height: 100%;
  width: auto;
  -webkit-transform: translate(-50%,-50%);
      -ms-transform: translate(-50%,-50%);
          transform: translate(-50%,-50%);
}
.people-name{
  font-family: sans-serif;
  font-size: 1.1rem;
  color: #777;
  font-weight: 700;
  margin: 0.5rem 0;
}
.people-position{
  font-style: italic;
  font-size: 0.8rem;
  color: #777;
  margin: 0.5rem 0;
}
.people-description{
  font-size: 0.9rem;
  font-style: italic;
  color: #aaaaaa;
  margin: 0.5rem 0;
}
.people-accounts{
  margin: 0.5rem 0;
}
</style>
