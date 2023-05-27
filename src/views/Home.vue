<template>
  <div>
    <SideBar @data-updated="handleDataUpdated" />
    <ImageContainer :selectedOption="selectedOption" :images="data"/>
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