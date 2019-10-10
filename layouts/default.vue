<template>
  <v-app>
    <v-navigation-drawer
      v-model="drawer"
      fixed
      app
      temporary
    >
      <v-list>
        <v-list-tile
          v-for="(item, i) in items"
          :key="i"
          :to="item.to"
          router
          exact
        >
          <v-list-tile-action>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-tile-action>
          <v-list-tile-content>
            <v-list-tile-title v-text="item.title" />
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-navigation-drawer>
    <v-toolbar
      app
      color="primary"
      dark
    >
      <v-toolbar-side-icon @click="drawer = !drawer" />
      <v-toolbar-title v-text="title" />
      <v-spacer />
      <v-btn
        icon
        @click="logout"
      >
        <v-icon>exit_to_app</v-icon>
      </v-btn>
    </v-toolbar>
    <v-content>
      <nuxt />
    </v-content>
    <v-footer
      :fixed="fixed"
      app
    >
      <span class="pl-2">El Camarón &copy; 2019</span>
    </v-footer>
  </v-app>
</template>

<script>
import axios from "axios"

export default {
  data() {
    return {
      clipped: false,
      drawer: false,
      fixed: false,
      items: [
        {
          icon: 'apps',
          title: 'Inicio',
          to: '/home'
        }
      ],
      miniVariant: true,
      right: true,
      rightDrawer: false,
      title: 'El Camarón',
      base_url: 'https://librodepesca.com/elcamaron/',
    }
  },
  methods: {
    logout() {
      localStorage.clear()
      this.$router.push({ name: 'index'})
    }
  }
}
</script>
