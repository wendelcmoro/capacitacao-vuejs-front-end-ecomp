<template>
  <v-content id="contactBackground" fluid>
    <v-layout row>
      <v-flex md12>
        <v-layout row>
          <v-flex md12>
            <div align="center">
              <h1 id="ContactTitle">Contact Us</h1>
            </div>
          </v-flex>
        </v-layout>
      </v-flex>
    </v-layout>
    <v-row>
      <v-col lg="12">
        <v-row>
          <v-col md="12">
            <div align="center">
              <p id="contactText">
                Magnam dolores commodi suscipit. Necessitatibus eius consequatur ex aliquid fuga eum quidem. Sit sint consectetur velit.
                Quisquam quos quisquam cupiditate. Et nemo qui impedit suscipit alias ea. Quia fugiat sit in iste officiis commodi cu dem hic quas.
              </p>
            </div>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
    <v-row>
      <v-col>
        <v-row>
          <v-col id="contactInfo" xs="12" sm="10" md="5" lg="3">
            <v-row>
              <div>
                <h1 id="contactCardTitle">
                  Amoeba
                </h1>
                <p id="contactCardText">
                  Cras fermentum odio eu feugiat. Justo eget magna
                  fermentum iaculis eu non diam phasellus. Scelerisque
                  felis imperdiet proin fermentum leo. Amet volutpat
                  consequat mauris nunc congue.
                </p>
              </div>
            </v-row>
            <v-row id="contactCardText">
              <v-cols cols="6">
                <div>
                  <v-avatar color="teal">
                    <v-avatar color="white" size="45">
                      <a href="https://www.twitter.com/"><v-icon color="teal" large>mdi-twitter</v-icon></a>
                    </v-avatar>
                  </v-avatar>
                  <v-avatar color="teal">
                    <v-avatar color="white" size="45">
                      <a href="https://www.facebook.com/"><v-icon color="teal" x-large>mdi-facebook</v-icon></a>
                    </v-avatar>
                  </v-avatar>
                  <v-avatar color="teal">
                    <v-avatar color="white" size="45">
                      <a href="https://www.instagram.com/"><v-icon color="teal" x-large>mdi-instagram</v-icon></a>
                    </v-avatar>
                  </v-avatar>
                  <v-avatar color="teal">
                    <v-avatar color="white" size="45">
                      <a href="https://www.linkedin.com/"><v-icon color="teal" x-large>mdi-linkedin</v-icon></a>
                    </v-avatar>
                  </v-avatar>
                </div>
              </v-cols>
            </v-row>
          </v-col>
          <v-col id="contactData" cols="12" sm="10" md="5" lg="2">
            <v-row>
              <v-col sm="1" md="2" lg="2">
                  <v-icon x-large color="teal">
                    mdi-map-marker
                  </v-icon>
              </v-col>
              <v-col sm="10" md="9" lg="9">
                  {{ contacts[0].endereco }}
              </v-col>
              <v-col sm="1" md="1" lg="2" />
            </v-row>
            <br>
            <v-row>
              <v-col sm="1" md="2"  lg="2">
                <v-icon x-large color="teal">
                  mdi-email
                </v-icon>
              </v-col>
              <v-col sm="10" md="9" lg="9">
                {{ contacts[0].email }}
              </v-col>
              <v-col sm="1" md="1"  lg="2" />
            </v-row>
            <br>
            <v-row>
              <v-col sm="1" md="2" lg="2">
                <v-icon x-large color="teal">
                  mdi-phone
                </v-icon>
              </v-col>
              <v-col sm="10" md="9"  lg="9">
                {{ contacts[0].telefone }}
              </v-col>
              <v-col sm="1" md="1"  lg="2" />
            </v-row>
          </v-col>
          <v-col id="contactFields" xs="12" sm="12" md="12" lg="4">
            <v-row>
              <v-col sm="11">
                <v-text-field v-model="messageData.nome" label="Your Name" :rules="[v => !!v || 'Name is required']" outlined background-color="white" />
              </v-col>
            </v-row>
            <v-row>
              <v-col sm="11">
                <v-text-field v-model="messageData.email" label="Your Email" :rules="[v => !!v || 'Email is required']" outlined background-color="white" />
              </v-col>
            </v-row>
            <v-row>
              <v-col sm="11">
                <v-text-field v-model="messageData.assunto" label="Subject" :rules="[v => !!v || 'Subject is required']" outlined background-color="white" />
              </v-col>
            </v-row>
            <v-row>
              <v-col sm="11">
                <v-textarea v-model="messageData.mensagem" label="Message" :rules="[v => !!v || 'Message is required']" outlined background-color="white" />
              </v-col>
            </v-row>
            <v-row sm="12">
                <v-col cols="3" />
                <v-col cols="4">
                  <v-btn x-large dark color="teal" @click="sendMessage()">
                    Send Message
                  </v-btn>
                </v-col>
                <v-col cols="4" />
            </v-row>
          </v-col>
        </v-row>
      </v-col>
    </v-row>
  </v-content>
</template>

<style>
#contactInfo {
  margin-left: 14%;
  padding-right: 1%;
}
#contactBackground {
    background-color:#f2f9f8 !important;
    padding-top: 0px;
    border: 0;
}
#ContactTitle {
    padding-top: 100px;
    padding-bottom: 0px;
    margin-left: 20%;
    font-family: "Lato";
    font-weight: 300;
    font-size: 2.5rem;
    padding-right: 20%;
    color: #787474;
}
#contactText {
    padding-bottom: 50px;
    padding-left: 15%;
    padding-right: 15%;
    font-family: "sans-serif";
    font-weight: normal;
    font-size: 21px;
    color: #787474;
}
#contactCardTitle {
    margin-top: 2%;
    font-family: "Lato";
    font-weight: 300;
    padding-bottom: 2%;
    color: teal;
}
#contactCardText {
    padding-bottom: 10px;
    font-family: "sans-serif";
    font-weight: normal !important;
    font-size: 18px;
    color: #787474;
}
#contactData {
    margin-top: 1%;
    margin-left: 0%;
    font-weight: normal !important;
    font-size: 24px;
    color: #787474;
}
#contactPersonal {
  font-family: "sans-serif";
  font-size: 20px;
}
@media only screen and (max-width: 1500px) {
  #contactData {
      margin-top: 1%;
      margin-left: 0%;
      font-weight: normal !important;
      font-size: 18px;
      color: #787474;
  }
}
@media only screen and (max-width: 1263px) {
  #contactFields {
      margin-top: 1%;
      margin-left: 5%;
      margin-right: 5%;
      font-weight: normal !important;
      font-size: 18px;
      color: #787474;
  }
}
@media only screen and (max-width: 959px) {
  #contactInfo {
    margin-left: 10%;
    padding-right: 15%;
  }
  #contactData {
    margin-top: 1%;
    margin-left: 10%;
    font-weight: normal !important;
    font-size: 18px;
    color: #787474;
  }
}
@media only screen and (max-width: 599px) {
  #contactInfo {
    margin-left: 15%;
    padding-right: 10%;
  }
  #contactData {
    margin-top: 1%;
    margin-left: 15%;
    padding-left: 0%;
    padding-right: 5%;
    font-weight: normal !important;
    font-size: 18px;
    color: #787474;
  }
}
</style>

<script>
export default {
  name: 'HomeContactUs',
  label: true,
  props: {
    contacts: Array
  },
  data: () => {
    return {
      messageData: {
        nome: '',
        email: '',
        assunto: '',
        mensagem: ''
      }
    }
  },
  created () {
    this.contacts.push({ id: 0, endereco: '', email: '', telefone: '' })
  },
  methods: {
    sendMessage () {
      this.$axios
        .$post('/Novamensagem', this.messageData)
        .catch(({ response }) => {
          const { mensagem, errosSecundarios: erros } = response.data
          const listaErros = erros ? `\n ${Object.values(erros).join('\n')}` : ''
          window.alert(`${mensagem}${listaErros}`)
        })
      if (this.messageData.nome !== '' && this.messageData.email !== '' && this.messageData.assunto !== '' && this.messageData.mensagem !== '') {
        window.alert('Message sent successfully')
      }
    }
  }
}
</script>
