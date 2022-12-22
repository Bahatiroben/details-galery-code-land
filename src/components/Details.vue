<template>
  <div class="container custom-color z-100 "
      :class="isMobile ? ' v-w bottom-0 left-0 absolute block' : 'w-2/5 mb-5 absolute flex ml-5 ' + bannerPosition"
      :style="{'color': detailsElementsColor}">
    <span class="top-0 left-0 right-0 bottom-0 hidden w-2/5 v-w" />
    <div 
      class="custom-bg-color details-container text-sm basis-full p-3"
      :class="isMobile ? '' : 'p-4'"
      :style="{'background-color': detailsBackgroundColor}">
      <div class="details-title">
        <div class="flex justify-between"
          :class="isMobile ? 'flex-col-reverse' : 'mb-4'">
          <h3 class="font-medium"
            >{{detailsTitle}}</h3>
          <span 
            class="pagination-details font-medium">{{currentSlide + 1}} / {{totalSlides}}</span>
        </div>
        <p v-html="mainDescription"/>
      </div>
      <hr v-show="seeMoreDescription" 
        :class="isMobile ? 'mt-2' : 'mb-4 mx-auto'"
        :style="{'background-color': detailsElementsColor, height: '1px', border: 'none'}" />
      <div v-show="seeMoreDescription" class="more-description-container"
        :class="isMobile ? 'mt-2' : ''">
        <div class="see-more-description-title-container flex justify-between mb-2">
          <h3 class="font-medium">{{isMoreInfoOpen ? 'Less Information' : moreInformationsCustomLabel}}</h3>
          <i @click="toggleLessMoreInfo" class="cursor-pointer see-more-description-icon fa fa-lg fa-lg font-medium opacity-60"
              :class="isMoreInfoOpen ? 'fa-minus' : 'fa-plus'"></i>
        </div>
        <p v-show="isMoreInfoOpen" v-html="seeMoreDescription"/>
      </div>
    </div>
    <div v-show="!isMobile" class="flex mx-2 flex-col justify-end basis-5">
      <div class="cursor-pointer custom-bg-color" @click="swipeNext">
        <i :style="{'background-color': detailsBackgroundColor}" class="cursor-pointer flex w-6 h-6 text-center items-center justify-center fa fa-angle-right fa-lg"></i>
      </div>
      <div class="cursor-pointer custom-bg-color" @click="swipePrevious">
        <i :style="{'background-color': detailsBackgroundColor}" class="flex w-6 h-6 text-center mt-2 items-center justify-center fa fa-angle-left fa-lg"></i>
      </div>
    </div>
  </div>
</template>

<script>
import { ref } from 'vue';
export default {
  props: {
    detailsTitle: String, 
    mainDescription: String,
    seeMoreDescription: String,
    bannerPosition: String,
    currentSlide: Number,
    totalSlides: Number,
    swiper: Object,
    detailsBackgroundColor: String,
    detailsElementsColor: String,
    moreInformationsCustomLabel: String,
    isMobile: Boolean,
    width: Number
  },
  setup(props) {
    let isMoreInfoOpen = ref(false)
    function toggleLessMoreInfo() {
      isMoreInfoOpen.value = !isMoreInfoOpen.value
    }
    
    function swipeNext() {
      const swiper = document.querySelector('.swiper').swiper;
      swiper.slideNext()
    }

    function swipePrevious() {
      const swiper = document.querySelector('.swiper').swiper;
      swiper.slidePrev()
    }
    return { ...props, isMoreInfoOpen, swipeNext, swipePrevious, toggleLessMoreInfo }
  },
}
</script>
