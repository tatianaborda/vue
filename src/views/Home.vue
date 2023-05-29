<template>
  <div class="home-container">
    <SideBar @data-updated="handleDataUpdated" />
      <div v-if="data.length === 0" class="welcome-container">
        <p>Welcome to the Mars Files! Please select a rover to load the images :)</p>
      </div>
      <div v-else>
        <ImageContainer :selectedOption="selectedOption" :images="data" />
      </div>
  </div>
</template>

<script>
import SideBar from "../components/SideBar.vue";
import ImageContainer from "../components/ImageContainer.vue";

export default {
  components: {
    SideBar,
    ImageContainer,
  },
  data() {
    return {
      data: [],
    };
  },
  methods: {
    handleDataUpdated(response) {
       this.data = response.data.photos;
    },
  },
};
</script>

<style>
.home-container {
  width: 100%;
  display: grid;
  grid-template-columns: 20% 70%;
  gap: 5%;
}
.welcome-container{
  display: flex;
  align-items: center;
  justify-content:center;
  font-family: sans-serif;
  color: grey;
  font-size: 25px;
}
</style>






