<template>
  <div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  mounted(){
      axios.get('https://api.nasa.gov/mars-photos/api/v1/rovers/curiosity/photos?sol=1000&api_key=DEMO_KEY')
        .then(response => console.log(response))
    }
}
</script>
