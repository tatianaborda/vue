<template>
    <section id="main" class="main-alt">
    <div v-for="image in images" :key="image.id">
      <img :src="image.img_src" />
    </div>
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
