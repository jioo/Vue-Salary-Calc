<template lang="html">
  <v-toolbar fixed class="cyan" dark>
    <v-toolbar-title class="mr-4">
      <v-btn
        flat dark
        @click="navigateTo({name: 'index'})">
          Salary App
      </v-btn>
    </v-toolbar-title>

    <!-- <v-toolbar-items>
      <v-btn flat dark>
        Browse
      </v-btn>
    </v-toolbar-items> -->

    <v-spacer></v-spacer>
  </v-toolbar>
</template>

<script>
export default {
  methods: {
    navigateTo (route) {
      this.$router.push(route)
    }
  }
}
</script>

<style lang="css">
.home {
  cursor: pointer;
}
</style>
