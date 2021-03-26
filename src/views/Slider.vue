<script>
import VueSlickCarousel from "vue-slick-carousel";
import "vue-slick-carousel/dist/vue-slick-carousel.css";
// optional style for arrows & dots
import "vue-slick-carousel/dist/vue-slick-carousel-theme.css";

import axios from "@/axios";
import BaseLayout from "@/components/BaseLayout";
import BaseSlider from "@/components/BaseSlider";
export default {
  components: {
    VueSlickCarousel,
    BaseLayout,
    BaseSlider,
  },
  data() {
    return {
      sliders: [],
      loading: true,
      settings: {
        arrows: true,
        dots: true,
        dotsClass: "slick-dots custom-dot-class",
        edgeFriction: 0.35,
        infinite: false,
        speed: 500,
        slidesToShow: 1,
        slidesToScroll: 1,
      },
    };
  },
  mounted() {
    this.getSliders();
  },
  methods: {
    async getSliders() {
      const response = await axios.get("https://picsum.photos/v2/list");
      this.sliders = response.data;
      this.loading = false;
    },
  },
};
</script>

<template>
  <BaseLayout>
    <VueSlickCarousel v-bind="settings" v-if="sliders.length">
      <div v-for="slider in sliders" :key="slider.id">
        <BaseSlider :image="slider.download_url" />
      </div>
      <template #prevArrow="arrowOption">
        <div class="custom-arrow">{{ arrowOption.currentSlide }}/{{ arrowOption.slideCount }}</div>
      </template>
      <template #customPaging="page">
        <div class="custom-dot">{{ page + 1 }}</div>
      </template>
    </VueSlickCarousel>
  </BaseLayout>
</template>

<style>
.opacity-40 {
  opacity: 0.4;
}
</style>