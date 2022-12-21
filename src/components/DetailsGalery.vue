<template>
  <swiper
    :slides-per-view="1"
    :space-between="50"
    :navigation="true"
    @swiper="onSwiper"
    @slideChange="onSlideChange"
    class="default-slider"
    :modules="modules"
    :loop="true"
    :pagination="{clickable: true}"
    :autoplay="{
      delay: 100000,
      disableOnInteraction: false,
      pauseOnMouseEnter: true
    }"
  >
    <SwiperSlide v-for="(imgDetails, index) in data.imageDetails" :key="imgDetails.imageNumber" :virtual-index="imgDetails.imageNumber">
      <img :src="imgDetails.desktopImage"/>
      <Details
        v-if="bannerPosition !== undefined"
        :detailsTitle="imgDetails.detailsTitle"
        :mainDescription="imgDetails.mainDescription"
        :seeMoreDescription="imgDetails.seeMoreDescription"
        :bannerPosition="bannerPosition"
        :currentSlide="index + 1"
        :totalSlides="data.imageDetails.length"
       />
    </SwiperSlide>
  </swiper>
</template>

<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation, Pagination, Autoplay} from 'swiper';
import data from '../data/index';
import Details from './Details'

import 'swiper/swiper.min.css';
import 'swiper/css/pagination';
import {ref} from 'vue';

export default {
  name: 'HelloWorld',
  components: {
    Swiper, SwiperSlide, Details
  },
  setup() {
      const onSwiper = (swiper) => {
        console.log(swiper);
      };
      const onSlideChange = (e) => {
        console.log(e)
      };
      const bannerPosition = data.bannerPosition?.split('-').reduce((prev, curr) => `${prev}${curr}-0 `, '');

      return {
        onSwiper,
        onSlideChange,
        data: ref(data), 
        modules: [Pagination, Navigation, Autoplay],
        bannerPosition,
      };
  },

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
