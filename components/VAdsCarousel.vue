<script lang="ts">
import { defineComponent } from '@nuxtjs/composition-api'

export default defineComponent({
  name: 'VAds',

  props: {
    ads: {
      type: Object,
      required: true,
    },
  },
  setup(props) {
    let sliders = []
    const sliderLink = props.ads?.link || ''

    sliders = [
      {
        id: 1,
        advertisement_id: props.ads.id,
        src: props.ads.content,
        link: props.ads.link
      },
    ].concat(props.ads.additionalAds)

    const sliderSettings = {
      infinite: true,
      arrows: false,
      dots: false,
      rows: 1,
      autoplay: true,
      autoplaySpeed: 5000,
      speed: 500,
      slidesToShow: 1,
      slidesToScroll: 1,
      swipeToSlide: true,
    }

    return {
      sliderSettings,
      sliders,
      adsType: props.ads.type,
      sliderLink,
    }
  },
})
</script>

<template>
  <div class="ads-carousel-container">
    <template v-if="adsType === 'image' && sliders.length">
      <VueSlickCarousel v-bind="sliderSettings">
        <div v-for="(slider, index) in sliders" :key="'slide_' + index">
          <a :href="sliderLink" target="_blank" rel="noopener noreferrer" class="block">
            <figure v-if="slider.src" class="relative">
              <v-img :src="slider.src" alt="" />
            </figure>
          </a>
        </div>
      </VueSlickCarousel>
    </template>
  </div>
</template>
