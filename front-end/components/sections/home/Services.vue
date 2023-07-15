<template>
  <v-container id="servicesBackground" class="ma-0" fluid>
    <div class="Services-header">
      <h1 class="Services-title">
        Services
      </h1>
      <p class="Services-text">
        Magnam dolores commodi suscipit. Necessitatibus eius consequatur ex aliquid fuga eum quidem. Sit sint consectetur velit. Quisquam quos quisquam cupiditate. Et nemo qui impedit suscipit alias ea. Quia fugiat sit in iste officiis commodi quidem hic quas.
      </p>
    </div>
    <v-row id="services" justify="center">
      <v-col
        v-for="service in services.dados"
        :key="service"
        cols="12"
        sm="6"
        md="6"
        lg="4"
      >
        <div class="Service-link">
          <img :src="path + service.imagem.caminho" style="width: 75%">
          <h2 class="Service-title">
            {{ service.servico }}
          </h2>
          <p class="Service-text" style="color: #777;">
            {{ service.descricao }}
          </p>
        </div>
      </v-col>
    </v-row>
  </v-container>
</template>

<script scoped>
export default {
  name: 'Services',
  props: {
    services: Array
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
#servicesBackground{
  background-color: #f2f9f8;
  padding: 3.5rem 1rem;
  text-align: center;
  color: #555;
}
@media (min-width: 600px) {
  #servicesBackground{
    padding: 3.5rem 2rem;
  }
}
@media (min-width: 960px) {
  #servicesBackground{
    padding: 3.5rem 8rem;
  }
}
.Services-header{
  color: #777;
}
.Service-link{
  transition: 0.3s;
  color: #343a40;
}
.Service-link:hover{
  color: #70b9b0;
}
.Services-title{
  font-family: "Lato";
  font-weight: normal;
  margin-bottom: 1rem;
  font-size: 2.5rem;
}
.Services-text{
  line-height: 1.5;
  opacity: 0.7;
  font-family: sans-serif;
}
.Service-title{
  text-transform: uppercase;
  font-size: 1.3rem;
}
.Service-text{
  font-weight: 300;
}
</style>
