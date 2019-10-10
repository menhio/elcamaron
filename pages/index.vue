<template>
  <div id="app">
  <v-app id="inspire">
    <v-content>
      <v-container
        fluid
        fill-height
      >
        <v-layout
          align-center
          justify-center
        >
          <v-flex
            xs12
            sm8
            md4
          >
            <v-card class="elevation-12">
              <v-toolbar
                color="primary"
                dark
                flat
              >
                <v-toolbar-title>El Camarón</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-tooltip bottom>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      icon
                      large
                      target="_blank"
                      v-on="on"
                    >
                      <v-icon>mdi-code-tags</v-icon>
                    </v-btn>
                  </template>
                  <span>Source</span>
                </v-tooltip>
                <v-tooltip right>
                  <template v-slot:activator="{ on }">
                    <v-btn
                      icon
                      large
                      href="https://codepen.io/johnjleider/pen/pMvGQO"
                      target="_blank"
                      v-on="on"
                    >
                      <v-icon>mdi-codepen</v-icon>
                    </v-btn>
                  </template>
                  <span>Codepen</span>
                </v-tooltip>
              </v-toolbar>
              <v-card-text>
                <v-form>
                  <v-text-field
                    label="Usuario"
                    name="login"
                    prepend-icon="person"
                    type="text"
                    v-model="username"
                  ></v-text-field>

                  <v-text-field
                    id="password"
                    label="Contraseña"
                    name="password"
                    prepend-icon="lock"
                    type="password"
                    v-model="password"
                  ></v-text-field>
                </v-form>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn color="primary" @click="login">Entrar</v-btn>
              </v-card-actions>
            </v-card>
          </v-flex>
        </v-layout>
      </v-container>
    </v-content>
  </v-app>
</div>
</template>

<script>
import axios from "axios"

export default {
  name: 'index',
  layout: 'empty',
  data() {
    return {
      username: 'admin',
      password: 'aQ4#lJQV#M',
      base_url: 'https://librodepesca.com/elcamaron/',
    }
  },
  methods: {
    login() {
      axios.post(this.base_url + 'user/login?_format=json',
      {
        'name': this.username,
        'pass': this.password
      })
      .then(res => {
        const encodedString = btoa(this.username + ':' + this.password);
        localStorage.encodedString = encodedString
        localStorage.uid = res.data.current_user.uid
        localStorage.name = res.data.current_user.name
        localStorage.csrf_token = res.data.csrf_token
        localStorage.logout_token = res.data.logout_token
        console.log(res.data)
        this.$router.push({ name: 'home'})
      })
      .catch(error => console.log(error))
    }
  }
}
</script>
