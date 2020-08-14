<template>
  <div>
    <div class="Container">

      <label for="country">Select a Country: </label>
      <b-form-select 
        v-model="selectedOne" 
        @change="pickedCountry(selectedOne)"
        class="mb-3">

        <b-form-select-option 
          v-for="country in countries"
          :key="country.id"
          :label="country.name"
          :value="country.id">
        </b-form-select-option>
      </b-form-select>

      <label for="state">Select a State: </label>
      <b-form-select 
        v-model="selectedTwo" 
        @change="pickedState(selectedTwo)"
        class="mb-3">

        <b-form-select-option 
          v-for="state in states"
          :key="state.id"
          :label="state.name"
          :value="state.id">
        </b-form-select-option>
      </b-form-select>

      <label for="city">Select a City: </label>
      <b-form-select 
        v-model="selectedThree" 
        @change="pickedCity(selectedThree)"
        class="mb-3">

        <b-form-select-option 
          v-for="city in cities"
          :key="city.id"
          :label="city.name"
          :value="city.id">
        </b-form-select-option>
      </b-form-select>

    </div>
  </div>
</template>

<script>
import axios from'axios'
import eventBus from '../state/eventBus.js'
export default {
  name: 'RequestComponent',
  created () {
    axios
      .get(
        "https://raw.githubusercontent.com/dr5hn/countries-states-cities-database/master/countries%2Bstates%2Bcities.json"
      )
      .then((response) => {
        this.countries = response.data;
      })
      .catch((error) => {
        error;
      })
  },

  data () {
    return {
      selectedCountry: "",
      selectedState: "",
      selectedCity: "",
      countries: [],
      states: [],
      cities: [],
    }
  },

  methods: {
    pickedCountry(selectedOne) {
      const country = this.countries.find((e) => e.id == selectedOne);
      this.states = country.states;
      eventBus.$emit("selected-country", country.name);
    },

    pickedState(selectedTwo) {
      const state = this.states.find((e) => e.id == selectedTwo);
      this.cities = state.cities;
      eventBus.$emit("selected-state", state.name)
    },

    pickedCity(selectedThree) {
      const city = this.cities.find((e) => e.id == selectedThree);
      eventBus.$emit("selected-city", city.name);
    }
  }

};
</script>

<style scoped>

</style>