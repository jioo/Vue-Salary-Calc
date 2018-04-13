<template lang="html">
  <v-card class="white elevation-4">
    <v-toolbar>
      <v-btn
      color="green"
      small
      absolute
      bottom
      left
      fab
      v-on:click="increment('x')"
      :disabled="y === 1"
      ><v-icon>+</v-icon>
      </v-btn>
      <v-card-title>
        Days: {{ x }}
      </v-card-title>
    </v-toolbar>
    <v-card-text>
      <v-list dense class="pt-5">
        <v-list-tile>
          <v-list-tile-content>Frist Cutoff:</v-list-tile-content>
          <v-list-tile-content class="align-end">{{ formatCurrency(firstCutoff) }}</v-list-tile-content>
        </v-list-tile>
        <v-divider></v-divider>
        <v-list-tile>
          <v-list-tile-content class="deduction">Tax:</v-list-tile-content>
          <v-list-tile-content class="align-end deduction">{{ formatCurrency(firstCutoffTax)}}</v-list-tile-content>
        </v-list-tile>
        <v-divider></v-divider>
        <v-list-tile>
          <v-list-tile-content class="pl-3 pt-2">
            <v-switch
            v-model="toggleDeduction1"
            ></v-switch>
          </v-list-tile-content>
          <v-list-tile-content>
            Apply Deduction
          </v-list-tile-content>
        </v-list-tile>
      </v-list>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  props: [

  ],
  data () {
    return {
      
    }
  }
}
</script>

<style lang="css">
</style>
