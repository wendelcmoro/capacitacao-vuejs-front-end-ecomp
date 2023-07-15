<template>
  <v-container id="aboutContainer" fluid>
    <div id="aboutSession">
      <div>
        <h2 id="aboutTitle">
          About Us
        </h2>
      </div>
    </div>
    <v-row>
      <v-col id="aboutInfo" xs="12" sm="12" md="12" lg="4">
        <h1 id="aboutCardTitle">
          Voluptatem dignissimos provident quasi corporis voluptates sit assumenda.
        </h1>
        <p id="aboutCardSubtitle">
          Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
        </p>
        <div id="aboutCardText">
          <p>
            <v-icon color="green">
              mdi-checkbox-marked-circle-outline
            </v-icon>
            Uilamco laboris nisi ut aliquip ex ea commodo consequat.
          </p>
          <p>
            <v-icon color="green">
              mdi-checkbox-marked-circle-outline
            </v-icon>
            Duis aute irure dolor in reprehenderit in voluptate velit.
          </p>
          <p>
            <v-icon color="green">
              mdi-checkbox-marked-circle-outline
            </v-icon>
            Ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate trideta storacalaperda mastiro dolore eu fugiat nulla pariatur.
          </p>
          <p>
            Ullamco laboris nisi ut aliquip ex ea commodo consequat.
            Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur.
            Excepeteur sint occaecat cupidatat  non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
          </p>
        </div>
      </v-col>
      <v-col id="aboutImageCol" xs="12" sm="12" md="12" lg="4">
        <v-img id="aboutImage" src="../../../imagens/about-img.jpg" />
      </v-col>
    </v-row>
  </v-container>
</template>

<style>

#aboutInfo {
  margin-left: 20%;
  padding-right: 2%;
}
#aboutContainer {
    margin-bottom: 0px;
    background-color: white;
}
#aboutImageCol {
    margin-top: 15px;
    padding-left: 1%;
}
#aboutImage {
  height: 90%;
}
#aboutCardText{
   font-size: 18px;
   color: #787474;
   font-family: "sans-serif";
}
#aboutCardSubtitle{
   font-size: 18px;
   color: #787474;
   font-style: italic;
   font-family: "sans-serif";
}
#aboutCardTitle {
    padding-bottom: 10px;
    font-weight: normal;
    font-size: 30px;
    color:  #787474;
    font-family: "sans-serif";
}
#aboutTitle {
    font-weight: normal;
    color:  #787474;
    padding-bottom: 50px;
    font-size: 2.5rem;
    font-family: "Lato";
}
#aboutSession {
    padding-top: 50px;
    padding-bottom: 0px;
    justify-content: center;
    align-items: center;
    display: flex;
}
@media only screen and (max-width: 1851px) {
  #aboutImage {
    height: 100%;
  }
}
@media only screen and (max-width: 1263px) {
  #aboutInfo {
    margin-left: 5%;
    margin-right: 15%;
    padding-right: 10%;
  }
}
@media only screen and (max-width: 600px) {
  #aboutInfo {
    margin-left: 1%;
    margin-right: 1%;
    padding-right: 0%;
  }
}

</style>

<script>
export default {
  name: 'HomeAboutUs'
}
</script>
