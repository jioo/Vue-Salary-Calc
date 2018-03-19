<template lang="html">
  <v-layout row wrap>

    <v-flex d-flex md5>
      <v-layout row wrap>
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
                v-model="salary"
              ></v-text-field>

              <v-text-field
                type="number"
                label="No. of Working Days"
                required
                :rules="[required]"
                v-model="days"
              ></v-text-field>
            </v-card-text>
          </v-card>
        </v-flex>
        <v-flex d-flex lg12>
          <v-layout row wrap>
            <v-flex d-flex lg6>
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
            </v-flex>
            <v-flex d-flex lg6>
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
                    Days: {{ y }}
                  </v-card-title>
                </v-toolbar>
                <v-card-text>
                  <v-list dense class="pt-5">
                    <v-list-tile>
                      <v-list-tile-content>Second Cutoff:</v-list-tile-content>
                      <v-list-tile-content class="align-end">{{ formatCurrency(secondCutoff) }}</v-list-tile-content>
                    </v-list-tile>
                    <v-divider></v-divider>
                    <v-list-tile>
                      <v-list-tile-content class="deduction">Tax:</v-list-tile-content>
                      <v-list-tile-content class="align-end deduction">{{ formatCurrency(secondCutoffTax)}}</v-list-tile-content>
                    </v-list-tile>
                    <v-divider></v-divider>
                    <v-list-tile>
                      <v-list-tile-content class="pl-3 pt-2">
                        <v-switch
                        v-model="toggleDeduction2"
                        ></v-switch>
                      </v-list-tile-content>
                      <v-list-tile-content>
                        Apply Deduction
                      </v-list-tile-content>
                    </v-list-tile>
                  </v-list>
                </v-card-text>
              </v-card>
            </v-flex>
          </v-layout>
        </v-flex>
      </v-layout>
    </v-flex>

    <v-flex md3>
      <v-layout row wrap>
        <v-flex d-flex md12>
          <v-card class="white elevation-4">

            <v-card-text>
              <v-layout row>
                <v-flex xs12>
                  <v-subheader><b>Deductions: </b>&nbsp;<span class="deduction">{{ formatCurrency(totalDeduction) }}</span></v-subheader>
                </v-flex>
              </v-layout>
              <v-layout row>
                <v-flex xs12>
                  <v-text-field
                    type="number"
                    label="Day(s)"
                    v-model="totaldeductPerDay"
                  ></v-text-field>

                  <v-text-field
                    type="number"
                    label="Hour(s)"
                    v-model="totaldeductPerHour"
                  ></v-text-field>

                  <v-text-field
                    type="number"
                    label="Minute(s)"
                    v-model="totaldeductPerMinute"
                  ></v-text-field>

                  <v-btn
                  color=""
                  v-on:click="reset()"
                  >Reset
                  </v-btn>
                </v-flex>
              </v-layout>
            </v-card-text>
          </v-card>
        </v-flex>

        <v-flex d-flex md12>
          <v-card class="elevation-2">
            <v-toolbar dense class="red lighten-2" dark>
              <v-toolbar-title>Deduction Table</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-data-table
                :items="deductionTableItems"
                class=""
                hide-actions
                hide-headers
                >
                <template slot="items" slot-scope="props">
                  <td>{{ props.item.label }}</td>
                  <td>{{ formatCurrency(props.item.value) }}</td>
                </template>
              </v-data-table>
            </v-card-text>
          </v-card>
        </v-flex>
      </v-layout>
    </v-flex>

    <v-flex d-flex md4>
      <v-layout row wrap>
        <v-flex md12>
          <v-card class="white elevation-4">
            <v-toolbar dense class="cyan" dark>
              <v-toolbar-title>Salary Result</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-layout row>
                <v-flex xs4>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="subheading">Monthly</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader class="subheading">Annual</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Basic Salary</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(monthlySalary) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(annualSalary) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Witholding Tax</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(monthlyTax) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(annualTax) }}</v-subheader>
                </v-flex>
              </v-layout>

              <v-layout row>
                <v-flex xs4>
                  <v-subheader>Net Pay</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(montlyNetPay) }}</v-subheader>
                </v-flex>
                <v-flex xs4>
                  <v-subheader>{{ formatCurrency(annualNetPay) }}</v-subheader>
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
      totaldeductPerDay: '',
      totaldeductPerHour: '',
      totaldeductPerMinute: '',
      totalDeduction: 0,
      toggleDeduction1: false,
      toggleDeduction2: false,
      deductionTableItems: [
        {
          label: 'Per Day',
          value: 0
        },
        {
          label: 'Per Hour',
          value: 0
        },
        {
          label: 'Per Minute',
          value: 0
        }
      ],
      required: (value) => !!value || 'This field is required.'
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
      if (this.toggleDeduction1) {
        this.firstCutoff -= this.totalDeduction
      }

      this.secondCutoffTax = (this.monthlyTax / this.days) * this.y
      this.secondCutoff = (this.perDay * this.y) - this.secondCutoffTax
      if (this.toggleDeduction2) {
        this.secondCutoff -= this.totalDeduction
      }
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
      this.deductionTableItems[0].value = this.deductPerDay

      this.deductPerHour = this.deductPerDay / 24
      this.deductionTableItems[1].value = this.deductPerHour

      this.deductPerMinute = this.deductPerHour / 60
      this.deductionTableItems[2].value = this.deductPerMinute
    },
    formatCurrency: function (value) {
      if (!isNaN(value)) {
        let val = (value / 1).toFixed(2).replace(',', '.')
        return val.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ',')
      } else {
        return 0.00
      }
    },
    computetotalDeduction: function () {
      this.totalDeduction = (this.totaldeductPerDay * this.deductPerDay) + (this.totaldeductPerHour * this.deductPerHour) + (this.totaldeductPerMinute * this.deductPerMinute)
    },
    reset: function () {
      this.totaldeductPerDay = ''
      this.totaldeductPerHour = ''
      this.totaldeductPerMinute = ''
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
      this.compute()
      this.setTaxDetails()
    },
    days: function (val) {
      this.compute()
    },
    totaldeductPerDay: function () {
      this.computetotalDeduction()
      this.setCutoff()
      this.setDeductionDetails()
    },
    totaldeductPerHour: function () {
      this.computetotalDeduction()
      this.setCutoff()
      this.setDeductionDetails()
    },
    totaldeductPerMinute: function () {
      this.computetotalDeduction()
      this.setCutoff()
      this.setDeductionDetails()
    },
    toggleDeduction1: function () {
      this.setCutoff()
      this.setDeductionDetails()
    },
    toggleDeduction2: function () {
      this.setCutoff()
      this.setDeductionDetails()
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
