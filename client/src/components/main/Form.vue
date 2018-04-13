<template lang="html">
  <v-flex d-flex md12>
    <v-card class="white elevation-4">
      <v-toolbar class="teal" dark>
        <v-toolbar-title>Salary Form</v-toolbar-title>
      </v-toolbar>
      <v-card-text>
        <v-text-field
        type="number"
        label="Basic Salary"
        required
        :rules="[required]"
        v-model="childSalary"
        ></v-text-field>

        <v-text-field
        type="number"
        label="No. of Working Days"
        required
        :rules="[required]"
        v-model="childDays"
        ></v-text-field>
      </v-card-text>
    </v-card>
  </v-flex>
</template>

<script>
export default {
  props: [
    'salary',
    'days'
  ],
  data () {
    return {
      childSalary: this.salary,
      childDays: this.days,
      required: (value) => !!value || 'This field is required.'
    }
  },
  watch: {
    childSalary: function (val) {
      this.$emit('salaryChanged', this.childSalary)
    },
    childDays: function (val) {
      this.$emit('daysChanged', this.childDays)
    }
  }
}
</script>

<style lang="css">
</style>
