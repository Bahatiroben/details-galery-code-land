<template>
  <div class="container z-10 flex w-2/5 absolute m-5" :class="bannerPosition">
    <span class="top-0 left-0 right-0 bottom-0 hidden" />
    <div class="details-container text-sm p-4 bg-white basis-full">
      <div class="details-title">
        <div class="flex justify-between mb-2">
          <h3 class="font-medium	">{{detailsTitle}}</h3>
          <span class="pagination-details font-medium	">{{currentSlide}} / {{totalSlides}}</span>
        </div>
        <p v-html="mainDescription"/>
      </div>
      <hr class="my-4 mx-auto" />
      <div class="more-description-container">
        <div class="see-more-description-title-container flex justify-between mb-2">
          <h3 class="font-medium	">Less Information</h3>
          <i class="cursor-pointer see-more-description-icon fa fa-lg fa-minus fa-lg font-medium opacity-60"></i>
        </div>
        <p v-html="seeMoreDescription"/>
      </div>
    </div>
    <div class="flex mx-2 flex-col justify-end basis-5">
      <i class="cursor-pointer flex bg-white w-6 h-6 text-center items-center justify-center fa fa-angle-right fa-lg"></i>
      <i class="cursor-pointer flex bg-white w-6 h-6 text-center mt-2 items-center justify-center fa fa-angle-left fa-lg"></i>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    detailsTitle: String, 
    mainDescription: String,
    seeMoreDescription: String,
    bannerPosition: String,
    currentSlide: Number,
    totalSlides: Number
  },
  setup(props) {
    return {...props}
  },
}
</script>