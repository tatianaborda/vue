<template>
  <div class="sidebar">
    <h1>
      <span>Rovers</span>
    </h1>
    <div>
  <select @change="handleOptionChange" v-model="selectedOption">
    <option value="" selected disabled>Please select one</option>
    <option value="curiosity">Curiosity</option>
    <option value="opportunity">Opportunity</option>
    <option value="spirit">Spirit</option>
  </select>
  </div>
  </div>
</template>

<script>
import axios from "axios"

export default {
  name: 'SideBar',
  data() {
    return {
      images: [],
    };
  },
  methods: {
    handleOptionChange(event) {
      const selectedValue = event.target.value;
      if (selectedValue === 'curiosity') {
        this.fetchDataFromAPI('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=DEMO_KEY');
      } else if (selectedValue === 'opportunity') {
        this.fetchDataFromAPI('https://api.nasa.gov/mars-photos/api/v1/rovers/opportunity/photos?sol=1000&api_key=DEMO_KEY');
      } else if (selectedValue === 'spirit') {
        this.fetchDataFromAPI('https://api.nasa.gov/mars-photos/api/v1/rovers/spirit/photos?sol=1000&api_key=DEMO_KEY');
      }
    },
    
    fetchDataFromAPI(apiEndpoint) {
      axios.get(apiEndpoint)
      .then(response => {
        this.images = response.data.photos;
        this.$emit('data-updated', response);
      })
      .catch(error => {
        console.log(error);
      });
    },
  }
}
</script>


<style scoped>
.sidebar {
  color: white;
  background-color: red;
  float: left;
  position: fixed;
  z-index: 1;
  top: 0;
  left: 0;
  bottom: 0;
  padding: 0.5em;
  display: flex;
  flex-direction: column;
}
.sidebar h1 {
  height: 2.5em;
}
</style>