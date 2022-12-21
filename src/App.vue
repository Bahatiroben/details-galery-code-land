<template>
  <DetailsGalery msg="{{data}}"/>
</template>

<script>
import DetailsGalery from './components/DetailsGalery.vue'
import data from './data/index';
export default {
  name: 'App',
  components: {
    DetailsGalery
  },
  data(){return data}
}
</script>

<style>

</style>
