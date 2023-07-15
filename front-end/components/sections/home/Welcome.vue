<template>
  <v-container id="welcomeBackground" fluid>
    <div id="apresentacao">
      <div>
        <h1 id="titulo" align="center">
          Welcome to Amoeba
        </h1>
      </div>
      <v-row cols="12">
        <v-col cols="2" />
        <v-col cols="8">
          <div id="texto">
            <p color="white" align="center">
              We are a team of talanted designers making websites with bootstrap
            </p>
          </div>
        </v-col>
        <v-col cols="2" />
      </v-row>
      <v-row cols="12">
        <v-col cols="4" />
        <v-col cols="4">
          <div id="getStarted">
            <v-btn
              class="text-none"
              width="200"
              rounded
              outlined
              x-large
              color="white"
              @click="$vuetify.goTo('#aboutContainer',0,2)"
            >
              Get Started
            </v-btn>
          </div>
        </v-col>
        <v-col cols="4" />
      </v-row>
    </div>
  </v-container>
</template>

<style>
#welcomeBackground {
    background-color: rgba(51,255,204,0.7);
    max-width: 100vw;
    height: 40%;
}
#apresentacao {
    padding-top: 10%;
    padding-bottom: 0px;
}
#titulo {
    justify-content: center;
    align-items: center;
    padding-top: 0%;
    display: flex;
    color: white;
    font-weight: 300;
    font-size: 3rem;
    font-family: "Roboto";
}
#texto {
    justify-content: center;
    align-items: center;
    display: flex;
    color: white;
    font-family: "sans-serif";
    font-size: 18px;
}
#getStarted {
    justify-content: center;
    align-items: center;
    display: flex;
    font-family: "sans-serif";
}
#welcomeImage {
    height: 100%;
}
.container {
        font-size: 1.3rem;
}
@media only screen and (max-width: 1500px) {
    #apresentacao {
        padding-top: 15%;
        padding-bottom: 0px;
    }
}
@media only screen and (max-width: 1200px) {
    #apresentacao {
        padding-top: 20%;
        padding-bottom: 0px;
    }
}
@media only screen and (max-width: 750px) {
    #apresentacao {
        padding-top: 25%;
        padding-bottom: 0px;
    }
}
@media only screen and (max-width: 500px) {
    #apresentacao {
        padding-top: 30%;
        padding-bottom: 0px;
    }
}

</style>
<script>
export default {
  name: 'HomeWelcome'
}
</script>
