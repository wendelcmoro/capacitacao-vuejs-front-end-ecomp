<template>
  <v-container id="callBackground" fluid>
    <div id="callTitle" align="center">
      <h1>Call To Action</h1>
    </div>
    <v-layout row>
      <v-flex md12>
        <v-layout row>
          <v-flex md12>
            <div id="callText">
              <p align="center">
                Duis aute irure dolor in reprehenderit in voluptate velit esse  cillum dolore eu fugiat nulla pariatur.
                Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
              </p>
            </div>
          </v-flex>
        </v-layout>
        <div id="calltoAction">
          <v-btn
            class="text-none"
            width="200"
            rounded
            outlined
            x-large
            color="white"
          >
            Call To Action
          </v-btn>
        </div>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<style>
#callBackground {
    background-color: rgba(0,102,102,0.2);
    max-width: 100%;
    padding: 3.5rem 1rem;
}
#callTitle {
    padding-top: 30px;
    color:  white;
}
#callText {
    justify-content: center;
    padding-left: 18%;
    padding-right: 18%;
    align-items: center;
    font-weight: normal;
    font-family: "sans-serif";
    font-size: 18px;
    color:  white;
}
#calltoAction {
    justify-content: center;
    align-items: center;
    display: flex;
}
</style>

<script>
export default {
  name: 'HomeCalltoAction'
}
</script>
