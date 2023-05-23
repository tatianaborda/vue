<template>
  <section id="main" class="main-alt">
    <button v-on:click="isVisible = !isVisible"> Curiosity </button>
    <div v-if="isVisible">
      <div v-for="curiosityImage in curiosityImages" :key="curiosityImage.id">
      <h2>{{curiosityImage.id}}</h2>
      <img :src="curiosityImage.img_src" />
      </div>
    </div>
    <button v-on:click="isVisible = !isVisible"> Opportunity </button>
    <div v-if="isVisible">
      <div v-for="opportunityImage in opportunityImages" :key="opportunityImage.id">
      <h2>{{opportunityImage.id}}</h2>
      <img :src="opportunityImage.img_src" />
      </div>
    </div>
    <button v-on:click="isVisible = !isVisible"> Spirit </button>
    <div v-if="isVisible">
      <div v-for="spiritImage in spiritImages" :key="spiritImage.id">
      <h2>{{spiritImage.id}}</h2>
      <img :src="spiritImage.img_src" />
      </div>
    </div>
  </section>
</template>

<script>
import axios from 'axios'

export default {
  data(){
    return {
      curiosityImages : [],
      opportunityImages : [],
      spiritImages : [], 
      isVisible: false
    }
  },
  mounted(){
    let curiosityURL = 'https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=DEMO_KEY';
    let opportunityURL = 'https://api.nasa.gov/mars-photos/api/v1/rovers/opportunity/photos?sol=1000&api_key=DEMO_KEY';
    let spiritURL = 'https://api.nasa.gov/mars-photos/api/v1/rovers/spirit/photos?sol=1000&api_key=DEMO_KEY';

    const curiosityRequest = axios.get(curiosityURL);
    const opportunityRequest = axios.get(opportunityURL);
    const spiritRequest = axios.get(spiritURL); 

    axios.all([
      curiosityRequest, 
      opportunityRequest, 
      spiritRequest])
      .then(axios.spread(function(curiosityImagesResponse, opportunityImagesResponse, spiritImagesResponse){
        const curiosityImages = curiosityImagesResponse.data.photos;
        const opportunityImages= opportunityImagesResponse.data.photos;
        const spiritImages = spiritImagesResponse.data.photos;
          console.log(curiosityImages);
          console.log(opportunityImages);
          console.log(spiritImages);
      }))
      .catch(function (error) {
        console.log(error);
      });
  }
}
</script>