<template>
  <div id="app">
    <v-app>
      <v-toolbar color="blue darken-2" dark fixed app>
        <v-toolbar-title>Salary Calculator</v-toolbar-title>
      </v-toolbar>
      <v-content>
        <v-container fluid grid-list-xl>
          <router-view></router-view>
        </v-container>
      </v-content>
      <v-footer class="blue darken-2 pt-4 pb-4">
        <v-layout row wrap align-center>
          <v-flex xs12>
            <div class="white--text ml-3 mx-auto subheading">
              <v-icon>code</v-icon>
               with
              <v-icon>favorite</v-icon>
               by
              <b>Justine Joshua Quiazon</b>
              &nbsp;
              - &nbsp;&nbsp;Powered By:
              <a href="https://vuejs.org/" target="_blank"><img src="https://avatars1.githubusercontent.com/u/6128107?s=400&v=4" alt="" width="25" height="25" class="mt-2"></a>
              <a href="https://vuetifyjs.com/en/" target="_blank"><img src="https://avatars0.githubusercontent.com/u/22138497?s=400&v=4" alt="" width="25" height="25"></a>
            </div>
          </v-flex>
        </v-layout>
      </v-footer>
    </v-app>
  </div>
</template>

<script>
import PageHeader from '@/components/Header'
export default {
  name: 'App',
  components: {
    PageHeader
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
</style>
