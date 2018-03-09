<template lang="html">
  <v-layout row wrap>
    <v-flex d-flex md12>
      <v-layout row wrap>
        <v-flex md4>
          <v-card class="white elevation-4">
            <v-toolbar class="teal" dark>
              <v-toolbar-title>Salary Form</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-text-field
                type="number"
                label="Basic Salary"
                v-model="salary"
              ></v-text-field>

              <v-text-field
                type="number"
                label="No. of Working Days"
                v-model="days"
              ></v-text-field>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex md4>
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
                <h1>Days: {{ x }} </h1>
              </v-card-title>
            </v-toolbar>
            <v-card-text>
              <v-layout row>
                <v-flex md6>
                  <v-subheader class="title">
                    First Cutoff:
                  </v-subheader>
                </v-flex>

                <v-flex md6>
                  <v-subheader class="title">
                    {{ formatCurrency(firstCutoff) }}
                  </v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex md6>
                  <v-subheader class="title">
                    <span class="deduction">Tax: </span>
                  </v-subheader>
                </v-flex>

                <v-flex md6>
                  <v-subheader class="title">
                    <span class="deduction">{{ formatCurrency(firstCutoffTax)}}</span>
                  </v-subheader>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
          <br />

          <v-card class="white elevation-4">
            <v-toolbar>
              <v-btn
              color="green"
              small
              absolute
              bottom
              left
              fab
              v-on:click="increment('y')"
              :disabled="x === 1"
              ><v-icon>+</v-icon>
              </v-btn>
              <v-card-title>
                <h1>Days: {{ y }} </h1>
              </v-card-title>
            </v-toolbar>
            <v-card-text>
              <v-layout row>
                <v-flex md6>
                  <v-subheader class="title">
                    Second Cutoff:
                  </v-subheader>
                </v-flex>

                <v-flex md6>
                  <v-subheader class="title">
                    {{ formatCurrency(secondCutoff) }}
                  </v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex md6>
                  <v-subheader class="title">
                    <span class="deduction">Tax: </span>
                  </v-subheader>
                </v-flex>

                <v-flex md6>
                  <v-subheader class="title">
                    <span class="deduction">{{ formatCurrency(secondCutoffTax)}}</span>
                  </v-subheader>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex md4>
          <v-card class="white elevation-4">

            <v-card-text>
              <v-layout row>
                <v-flex xs12>
                  <v-subheader class="title"><b>Deductions: </b>&nbsp;<span class="deduction">{{ formatCurrency(deduct1) }}</span></v-subheader>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <v-text-field
                    type="number"
                    label="Day(s)"
                    v-model="deductPerDay1"
                  ></v-text-field>

                  <v-text-field
                    type="number"
                    label="Hour(s)"
                    v-model="deductPerHour1"
                  ></v-text-field>

                  <v-text-field
                    type="number"
                    label="Minute(s)"
                    v-model="deductPerMinute1"
                  ></v-text-field>

                  <v-btn
                  color=""
                  v-on:click="reset1()"
                  :disabled="y === 1"
                  >Reset
                  </v-btn>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>

      </v-layout>
    </v-flex>

    <v-flex md12>
      <v-layout row wrap>
        <v-flex md8>
          <v-card class="white elevation-4">
            <v-toolbar dense class="cyan" dark>
              <v-toolbar-title>Tax Result</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-layout row>
                <v-flex xs4>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="headline">Monthly</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="headline">Annual</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader class="title">Basic Salary</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(monthlySalary) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(annualSalary) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader class="title">Witholding Tax</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(monthlyTax) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(annualTax) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader class="title">Net Pay</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(montlyNetPay) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="title">{{ formatCurrency(annualNetPay) }}</v-subheader>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex md4>
          <v-card class="white elevation-4">
            <v-toolbar dense class="red lighten-2" dark>
              <v-toolbar-title>Deduction Table</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-layout row>
                <v-flex xs6>
                  <v-subheader class="title">Per Day</v-subheader>
                </v-flex>
                <v-flex xs6>
                  <v-subheader class="title">{{ formatCurrency(deductPerDay) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs6>
                  <v-subheader class="title">Per Hour</v-subheader>
                </v-flex>
                <v-flex xs6>
                  <v-subheader class="title">{{ formatCurrency(deductPerHour) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs6>
                  <v-subheader class="title">Per Minute</v-subheader>
                </v-flex>
                <v-flex xs6>
                  <v-subheader class="title">{{ formatCurrency(deductPerMinute) }}</v-subheader>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  data () {
    return {
      salary: '',
      days: '',
      x: 0,
      y: 0,
      firstCutoff: 0,
      secondCutoff: 0,
      firstCutoffTax: 0,
      secondCutoffTax: 0,
      firstCutoffDeduc: 0,
      secondCutoffDeduc: 0,
      perDay: 0,
      monthlySalary: 0,
      annualSalary: 0,
      monthlyTax: 0,
      annualTax: 0,
      montlyNetPay: 0,
      annualNetPay: 0,
      deductPerDay: 0,
      deductPerHour: 0,
      deductPerMinute: 0,
      deductPerDay1: '',
      deductPerHour1: '',
      deductPerMinute1: '',
      deduct1: 0,
      deduct2: 0
    }
  },
  methods: {
    compute: function () {
      this.perDay = this.salary / this.days
      this.perDay = Math.round(this.perDay * 100) / 100 // roundoff

      this.x = Math.floor(this.days / 2)
      this.y = Math.ceil(this.days / 2)

      this.setCutoff()
      this.setDeductionDetails()
    },
    increment: function (value) {
      if (this.x === 0 || this.y === 0) return
      if (value === 'x') {
        this.x++
        this.y--
      } else {
        this.x--
        this.y++
      }
    },
    setCutoff: function () {
      this.firstCutoffTax = (this.monthlyTax / this.days) * this.x
      this.firstCutoff = (this.perDay * this.x) - this.firstCutoffTax

      this.secondCutoffTax = (this.monthlyTax / this.days) * this.y
      this.secondCutoff = (this.perDay * this.y) - this.secondCutoffTax
    },
    setTaxDetails: function () {
      this.monthlySalary = this.salary
      this.annualSalary = this.monthlySalary * 12
      var taxable = (this.annualSalary - 250000)

      if (taxable > 0) {
        this.annualTax = taxable * 0.08
        this.monthlyTax = this.annualTax / 12
      } else {
        this.annualTax = 0
        this.monthlyTax = 0
      }

      this.montlyNetPay = this.monthlySalary - this.monthlyTax
      this.annualNetPay = this.annualSalary - this.annualTax
    },
    setDeductionDetails: function () {
      this.deductPerDay = this.perDay
      this.deductPerHour = this.deductPerDay / 24
      this.deductPerMinute = this.deductPerHour / 60
    },
    formatCurrency: function (value) {
      let val = (value / 1).toFixed(2).replace(',', '.')
      return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
    },
    computeDeduct1: function () {
      this.deduct1 = (this.deductPerDay1 * this.deductPerDay) + (this.deductPerHour1 * this.deductPerHour) + (this.deductPerMinute1 * this.deductPerMinute)
    },
    reset1: function () {
      this.deductPerDay1 = ''
      this.deductPerHour1 = ''
      this.deductPerMinute1 = ''
    },
    reset2: function () {
      this.deductPerDay2 = ''
      this.deductPerHour2 = ''
      this.deductPerMinute2 = ''
    }
  },
  watch: {
    x: function (val) {
      this.setCutoff()
    },
    y: function (val) {
      this.setCutoff()
    },
    salary: function (val) {
      if (val !== '' && this.days !== '') {
        this.compute()
      }

      this.setTaxDetails()
    },
    days: function (val) {
      if (val !== '' && this.salary !== '') {
        this.compute()
      }
    },
    deductPerDay1: function () {
      this.computeDeduct1()
    },
    deductPerHour1: function () {
      this.computeDeduct1()
    },
    deductPerMinute1: function () {
      this.computeDeduct1()
    }
  }
}
</script>

<style lang="css">
.error {
  color: red;
}

.deduction {
  color: red;
}
</style>
