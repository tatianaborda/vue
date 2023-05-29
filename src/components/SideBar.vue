<template>
  <aside class="sidebar-container">
    <h1>
      <span>Rovers</span>
    </h1>
    <div>
      <select @change="handleOptionChange" v-model="selectedOption" class="select-dropdown">
        <option value="" selected disabled>Please select one</option>
        <option value="curiosity">Curiosity</option>
        <option value="opportunity">Opportunity</option>
        <option value="spirit">Spirit</option>
      </select>
    </div>
  </aside>
</template>

<script>
import axios from "axios";
import { throttle } from "lodash";

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
    
    fetchDataFromAPI: throttle(function(apiEndpoint) {
      axios.get(apiEndpoint)
      .then(response => {
        this.images = response.data.photos;
        this.$emit('data-updated', response);
      })
      .catch(error => {
        console.log(error);
      });
    }, 1000),
  }
}
</script>

<style scoped>
.sidebar-container{
  padding: 1rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
.select-dropdown{
  color: grey;
  padding: 16px;
  font-size: 16px;
  cursor: pointer;
  font-family: sans-serif;
}
h1{
  color: grey;
  font-size: 25px;
  font-family: sans-serif;
}

</style>