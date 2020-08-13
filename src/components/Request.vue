<template>
  <div>
    <div class="Container">

      <label for="country">Select a Country: </label>
      <select
        v-model="selectedCountry"
        @change="pickedCountry(selectedCountry)"
        
        
        >

        <option 
          v-for="country in countries"
          :key="country.id"
          :label="country.name"
          :value="country.id">
          
        </option>
      </select>

      <div>

        <label for="state">Select a State: </label>
        <select 
          @change="pickedState(selectedState)"
          v-model="selectedState"
          aria-placeholder="Select a State"
          >

          <option 
            v-for="state in states"
            :key="state.id"
            :label="state.name"
            :value="state.id">
            
          </option>
        </select>
      </div>
      
      <div>

        <label for="city">Select a City: </label>
        <select 
          @change="pickedCity(selectedCity)"
          v-model="selectedCity"
          aria-placeholder="Select a City"
          >

          <option 
            v-for="city in cities"
            :key="city.id"
            :label="city.name"
            :value="city.id">
            
          </option>
        </select>
      </div>

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
    pickedCountry(selectedCountry) {
      const country = this.countries.find((e) => e.id == selectedCountry);
      this.states = country.states;
      eventBus.$emit("selected-country", country.name);
    },

    pickedState(selectedState) {
      const state = this.states.find((e) => e.id == selectedState);
      this.cities = state.cities;
      eventBus.$emit("selected-state", state.name)
    },

    pickedCity(selectedCity) {
      const city = this.cities.find((e) => e.id == selectedCity);
      eventBus.$emit("selected-city", city.name);
    }
  }

};
</script>

<style scoped>

</style>