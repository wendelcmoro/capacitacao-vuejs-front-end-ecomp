<template>
  <v-container id="footerBackground" fluid>
    <v-col
      id="footerText"
      class="text-center"
      cols="12"
    >
      <span style="color: white;">&copy; Copyright <span style="font-weight: bold;">Amoeba</span>. All Rights Reserved</span>
      <br>
      <p style="padding: 10px;color: white;">
        Designed by <a href="https://bootstrapmade.com/" style="color:teal;text-decoration:none;">BootstrapMade</a>
      </p>
    </v-col>
  </v-container>
</template>

<style>
#footerBackground {
    border: 0px;
    background-color: #2d6760;
    max-width: 100%;
    height: 140px;
    font-size: 18px;
}
#footerText {
  padding-top: 30px;
}
@media only screen and (max-width: 354px) {
#footerBackground  {
    border: 0px;
    background-color: #2d6760;
    max-width: 100%;
    height: 140px;
    font-size: 14px !important;
}
}
</style>

<script>
export default {
  name: 'HomeCalltoAction'
}
</script>
