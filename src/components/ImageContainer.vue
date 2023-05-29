<template>
  <section class="image-wrapper">
    <article v-for="image in images" :key="image.id" class="image-container">
      <img :src="image.img_src" alt="Mars Rover Image" class="image">
    </article>
  </section>
</template>

<script>
export default {
  props: {
    images: {
      type: Array,
      required: true
    },
    selectedOption: {
      type: String,
      required: true
    }
  }
}
</script>

<style>
.image-wrapper{
  flex-wrap: wrap;
  flex: 1;
  display:flex;
}
.image-container {
  flex:1;
  min-width:30%;
  margin: 1rem;
  padding: 0.5rem;
}
.image{
  width: 100%;
}
</style>