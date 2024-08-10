<script lang="ts">
import { computed, defineComponent, PropType } from '@nuxtjs/composition-api';
import { breakpointsTailwind, useBreakpoints } from '@vueuse/core'
import { Advertisement } from '~/types/ads';

export default defineComponent({
  name: 'VAds',

  props: {
    ads: {
      type: Object as PropType<Advertisement>,
      required: true,
    }
  },

  setup(props) {
    const breakpoints = useBreakpoints(breakpointsTailwind)

    return {
      image: computed(() => props.ads.type === 'image'),
      video: computed(() => props.ads.type === 'video'),
      document: computed(() => props.ads.type === 'document'),
      iframe: computed(() => props.ads.type === 'iframe'),
      isMobile: breakpoints.smaller('sm'),
    }
  },
});
</script>

<template>
  <div>
    <template v-if="image">
      <template v-if="ads.isExternal">
        <template v-if="isMobile && ads.hasMobileContent">
          <a
            :href="ads.mobileLink"
            target="_blank"
            rel="noopener noreferrer"
            class="block"
          >
            <figure>
              <v-img :src="ads.mobileContent" />
            </figure>
          </a>
        </template>
        <template v-else>
          <a
            :href="ads.link"
            target="_blank"
            rel="noopener noreferrer"
            class="block"
          >
            <figure>
              <v-img :src="ads.content" />
            </figure>
          </a>
        </template>
      </template>
      <template v-else>
        <template v-if="isMobile && ads.hasMobileContent">
          <a
            :href="ads.mobileLink"
            target="_self"
            rel="noopener noreferrer"
            class="block"
          >
            <figure>
              <v-img :src="ads.mobileContent" />
            </figure>
          </a>
        </template>
        <template v-else>
          <a
            :href="ads.link"
            target="_self"
            rel="noopener noreferrer"
            class="block"
          >
            <figure>
              <v-img :src="ads.content" />
            </figure>
          </a>
        </template>
      </template>
    </template>
  </div>
</template>