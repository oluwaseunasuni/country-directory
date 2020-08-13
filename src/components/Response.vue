<template>
  <div>
    <p>
      Country Selected: {{ country }}
      <br/>
      Country Selected: {{ state }}
      <br/>
      Country Selected: {{ city }}

    </p>
  </div>
</template>

<script>
import eventBus from '../state/eventBus.js'
export default {
  name: 'ResponseComponent',
  data() {
    return {
      country: "",
      state: "",
      city: ""
    }
  },

  created() {
    eventBus.$on("selected-country", value => {
      this.country = value;
    });
    eventBus.$on("selected-state", value => {
      this.state = value;
    });
    eventBus.$on("selected-city", value => {
      this.city = value;
    });
  }
}
</script>