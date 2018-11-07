<template>
  <v-container>
    <v-layout
      text-xs-center
      wrap
    >
      <v-flex xs12>
        <v-img
          :src="require('../assets/bdaalogo.png')"
          class="my-3"
          contain
          height="100"
        ></v-img>
      </v-flex>

      <v-flex mb-4>
        <h1 class="display-2 font-weight-bold mb-3">
          Investment Calculator
        </h1>
        <p class="subheading font-weight-regular">
          Help us recommend you a good investment strategy by answering a few questions!
        </p>
      </v-flex>
    </v-layout>
    <v-layout align-center>
      <!--Form element asking user questions-->
      <v-flex md6 offset-md3>
        <v-form ref="form" v-model="valid" lazy-validation>
          <p class="body-2">What's your name?</p>
          <v-text-field
            v-model="name"
            :rules="nameRules"
            label="Full Name"
            required
          ></v-text-field>
          <p class="body-2">How many years would you like this investment to be active?</p>
          <v-text-field
            v-model="investmentPeriod"
            :rules="[num => num > 0 || 'Investment Period must be greater than zero']"
            label="Investment Period"
            required
          ></v-text-field>
          <p class="body-2">How many dollars are you going to invest this year?</p>
          <v-text-field
            v-model="investmentAmount"
            :rules="[num => num > 1000 || 'Required to invest at least $1000']"
            label="Investment Amount"
          ></v-text-field>
          <p class="body-2">Select from the dropdown the type of stocks do you want to invest in</p>
          <v-select
            v-model="stockType"
            :items="stockTypes"
            label="Stock Types"
            required
          ></v-select>
          <v-btn
            :disabled="!valid"
            @click="submit"
          >
            submit
          </v-btn>
          <v-btn @click="clear">clear</v-btn>
        </v-form>
      </v-flex>
    </v-layout>
  </v-container>
</template>

<script>
  export default {
    data: () => ({
      valid: true,
      name: '',
      nameRules: [
        n => !!n || 'Name is required',
        n => n.split(' ').length === 2 || 'First and last name required'
      ],
      investmentPeriod: 0,
      investmentAmount: 0,
      stockType: '',
      stockTypes: [
        'Single Company',
        'ETF',
        'Mutual Funds'
      ]
    }),
    methods: {
      submit() {
        // Use Fetch for API requests
        console.log(`User entered ${this.name}, ${this.investmentPeriod}, ${this.investmentAmount}, ${this.stockType}`);
      },
      clear() {
        this.$refs.form.reset();
        console.log('Clearing form');
      }
    }
  }
</script>

<style>

</style>
