<template>
  <div class="h-screen">
    <Details
      v-if="bannerPosition !== undefined"
      :detailsTitle="data.imageDetails[currentSlide].detailsTitle"
      :mainDescription="data.imageDetails[currentSlide].mainDescription"
      :seeMoreDescription="data.imageDetails[currentSlide].seeMoreDescription"
      :bannerPosition="bannerPosition"
      :currentSlide="currentSlide"
      :totalSlides="data.imageDetails.length"
      :detailsBackgroundColor="data.detailsBackgroundColor"
      :detailsElementsColor="data.detailsElementsColor"
      :moreInformationsCustomLabel="data.moreInformationsCustomLabel"
      :isMobile="isMobile"
    />
    <swiper
      v-if="data.showGalleryComponent"
      :slides-per-view="1"
      :navigation="true"
      class="default-slider"
      :style="{
        height: isMobile ? '83%' : '100vh'
      }"
      :modules="modules"
      :loop="loop"
      :pagination="{clickable: false}"
      @slideChange="slideChange"
      :autoplay="{
        delay: data.singleCardAutoplayTime * 1000,
        disableOnInteraction: false,
        pauseOnMouseEnter: false
      }"
    >
      <SwiperSlide 
        v-for="(imgDetails) in data.imageDetails" :key="imgDetails.imageNumber" :virtual-index="imgDetails.imageNumber">
        <div 
          v-show="!data.disableAutoplay && !isMobile"
          class="z-100 progress-bar absolute top-0 left-0"
          :style="{
            'background-color': data.progressBarColor,
            'animation-duration':`${data.singleCardAutoplayTime * 1000}ms`,
          }"></div>
        <img
          class="object-cover"
          :class="isMobile ? 'h-full' : 'h-screen'"
          :src="imgDetails[imageSrcKey]"/>
        </SwiperSlide>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { ref, computed } from 'vue';
import { Navigation, Pagination, Autoplay} from 'swiper';
import data from '../data/index';
import Details from './Details'

import 'swiper/swiper.min.css';
import 'swiper/css/pagination';
import { useWindowSize } from '@vueblocks/vue-use-core'


export default {
  name: 'DetailsGalery',
  components: {
    Swiper, SwiperSlide, Details
  },
  setup() {
      const width = ref(useWindowSize().width)
      const bannerPosition = ref(data.bannerPosition === 'center' ? 'left-1/4 top-1/3' : data.bannerPosition?.split('-').reduce((prev, curr) => `${prev}${curr}-0 `, ''));
      const currentIndex = ref(0);

      const isMobile = computed(() => width.value < 500)
      const isTablet = computed(() => width.value > 500 && width.value < 800)
      const isDesktop = computed(() => width.value > 800);
      
      const imageSrcKey = computed(() => {
        const currentImageDetails = data.imageDetails[currentIndex.value]
        if(isMobile.value && currentImageDetails.mobileImage) {
          return 'mobileImage'
        } else if(isTablet.value && currentImageDetails.tabletImage) {
          return 'tabletImage'
        } else if(isDesktop.value && currentImageDetails.desktopImage) {
          return 'desktopImage'
        } else {
          return 'desktopImage'
        }
      })
      async function slideChange(swiper) {
        currentIndex.value = swiper.realIndex
      }

      const modules = computed(() =>  [Navigation, isMobile.value === true ? Pagination : Navigation, !data.disableAutoplay ? Autoplay: Navigation])
      console.log(modules.value)
      return {
        data,
        isMobile,
        modules,
        bannerPosition,
        loop: !data.disableInfinityScroll,
        slideChange,
        currentSlide: currentIndex,
        imageSrcKey
      };
  },

}
</script>

<style scoped>
  .progress-bar {
    animation-timing-function: linear;
    animation-name: progress;
    animation-iteration-count: infinite;
    z-index: 100;
  }

  @keyframes progress {
    0% {width: 0%; height: 4px}
    100% {width: 100%; height: 4px}
  }
</style>
