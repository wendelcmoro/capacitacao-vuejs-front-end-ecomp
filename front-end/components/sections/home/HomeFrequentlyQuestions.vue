<template>
  <v-content id="frequentBackground" fluid>
    <v-layout row>
      <v-flex md12>
        <v-layout row>
          <v-flex md12>
            <div align="center">
              <h1 id="frequentTitle">Frequently Asked Questions</h1>
            </div>
          </v-flex>
        </v-layout>
        <div>
          <v-layout row>
            <v-flex 2.5 />
            <v-flex md7>
              <v-expansion-panels id="aboutPainel" accordion flat tile>
                <v-expansion-panel
                  v-for="item in frequentQuestion"
                  :key="item.num"
                >
                  <v-expansion-panel-header id="frequentQuestion" color="#f2f9f8" @click="frequentAnswer(item.num)">
                    <div id="frequentElement">
                      <v-icon id="frequentElement" :color="item.color" left>
                        {{ item.icon }}
                      </v-icon>
                      <span id="frequentElement" :style="{color: item.color}">
                        {{ item.question }}
                      </span>
                    </div>
                  </v-expansion-panel-header>
                  <v-expansion-panel-content color="#f2f9f8">
                    <span id="frequentText" style="color: #787474;">{{ item.text }}</span>
                  </v-expansion-panel-content>
                </v-expansion-panel>
              </v-expansion-panels>
            </v-flex>
            <v-flex 2.5 />
          </v-layout>
        </div>
      </v-flex>
    </v-layout>
  </v-content>
</template>

<style>
.v-expansion-panel-header__icon {
  display: none !important;
}
#frequentBackground {
    background-color:#f2f9f8 !important;
    padding-top: 0px;
    border: 0;
}
#frequentTitle {
    padding-top: 100px;
    padding-bottom: 50px;
    margin-left: 20%;
    padding-right: 20%;
    font-weight: 300;
    font-family: "Lato";
    font-size: 2.5rem;
    color: #787474;
}
#frequentQuestion {
  font-size: 20px;
  font-family: "sans-serif";
}
#frequentText {
    font-size: 15.5px;
    font-family: "sans-serif";
}
#frequentElement:hover {
  color: #276e5c;
}
@media only screen and (max-width: 959px) {
    #aboutPainel {
        padding-left: 5%;
        padding-right: 5%;
    }
}
</style>

<script>
export default {
  name: 'HomeFrequentlyQuestions',
  data: () => ({
    frequentQuestion: [
      { num: 0, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Non consectetur a reat nam at lectus urna duis?', text: 'Feugiat pretium nibh ipsum consequat. Tempus iaculis urna id volupat lacus laoreet non curabitur gravida. Venenatis lectus magna fringilla urna porttitor rhoncus dolor purus non.' },
      { num: 1, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Feugiat scelerisque varius morbi enim nunc faucibus a pellentesque?', text: 'Dolor sit amet consectetur adipiscing elit pellentesque habitant morbi. Id interdum velit laoreet id donec ultrices. Fringilla phasellus faucibus scelerisque eleifend donec pretium. Est pellentesque elit ullamcorper dignissim. Mauris ultrices eros in cursus turpis massa tincidunt dui.' },
      { num: 2, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Dolor sit amet consectetur adipiscing elit pellentesque habitant morbi?', text: 'Eleifend mi in nulla posuere sollicitudin aliquam ultrices sagittis orci. Faucibus pulvinar elementum integer enim. Sem nulla pharetra diam sit amet nisl suscipit. Rutrum tellus pellentesque eu tincidunt. Lectus urna duis convallis convallis tellus. Urna molestie at elementum eu facilisis sed odio morbi quis' },
      { num: 3, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Ac odio tempor orci dapibus. Aliquam eleifend mi in nulla?', text: 'Dolor sit amet consectetur adipiscing elit pellentesque habitant morbi. Id interdum velit laoreet id donec ultrices. Fringilla phasellus faucibus scelerisque eleifend donec pretium. Est pellentesque elit ullamcorper dignissim. Mauris ultrices eros in cursus turpis massa tincidunt dui.' },
      { num: 4, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Tempus quam pellentesque nec nam aliquam sem et tortor consequat?', text: 'Molestie a iaculis at erat pellentesque adipiscing commodo. Dignissim suspendisse in est ante in. Nunc vel risus commodo viverra maecenas accumsan. Sit amet nisl suscipit adipiscing bibendum est. Purus gravida quis blandit turpis cursus in' },
      { num: 5, icon: 'mdi-chevron-down', hide: true, color: 'black', question: 'Tortor vitae purus faucibus ornare. Varius vel pharetra vel turpis nunc eget lorem dolor?', text: 'Laoreet sit amet cursus sit amet dictum sit amet justo. Mauris vitae ultricies leo integer malesuada nunc vel. Tincidunt eget nullam non nisi est sit amet. Turpis nunc eget lorem dolor sed. Ut venenatis tellus in metus vulputate eu scelerisque. Pellentesque diam volutpat commodo sed egestas egestas fringilla phasellus faucibus. Nibh tellus molestie nunc non blandit massa enim nec.' }
    ]
  }),
  methods: {
    frequentAnswer (index) {
      let i = 0
      if (this.frequentQuestion[index].hide === true) {
        this.frequentQuestion[index].hide = false
        this.frequentQuestion[index].color = 'teal'
        this.frequentQuestion[index].icon = 'mdi-chevron-up'
      } else {
        this.frequentQuestion[index].hide = true
        this.frequentQuestion[index].color = 'black'
        this.frequentQuestion[index].icon = 'mdi-chevron-down'
      }
      for (i = 0; i < this.frequentQuestion.length; i++) {
        if (this.frequentQuestion[i].hide === false && this.frequentQuestion[i].question !== this.frequentQuestion[index].question) {
          this.frequentQuestion[i].hide = true
          this.frequentQuestion[i].color = 'black'
          this.frequentQuestion[i].icon = 'mdi-chevron-down'
        }
      }
    }
  }
}
</script>
