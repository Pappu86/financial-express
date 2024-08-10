<script lang="ts">
import {
  defineComponent,
  PropType,
  ref,
  useContext,
} from '@nuxtjs/composition-api'
import { useIntersectionObserver } from '@vueuse/core'

import { PostPagination, Posts } from '~/types/posts'
import { CategoryViewsChild } from '~/types/category'
import { Advertisement } from '~/types/ads'

export default defineComponent({
  name: 'CategoryViewsReview',

  props: {
    category: {
      type: String,
      required: true,
    },
    subcategory: {
      type: String,
      required: true,
    },
    url: {
      type: String,
      default: '/',
    },
    ads: {
      type: Object as PropType<Advertisement>,
      default: null,
    },
  },

  setup() {
    const { $axios, i18n } = useContext()

    const target = ref(null)
    const loading = ref(false)

    const posts = ref<Posts[]>([])
    const morePosts = ref<Posts[]>([])
    const nextPageUrl = ref(`api/en/category/views/reviews`)
    const hasPages = ref(true)
    const lang = i18n?.locale === 'bangla' ? 'bn' : 'en'

    const fetch = async () => {
      loading.value = true
      try {
        const response: CategoryViewsChild =
          await $axios.$get<CategoryViewsChild>(
            `api/${lang}/category/views/reviews`
          )

        nextPageUrl.value = `api/${lang}/category/views/sub-more/reviews/${response.id}`
        posts.value = [response.featured, ...response.posts]
      } finally {
        loading.value = false
      }
    }

    const { stop } = useIntersectionObserver(
      target,
      ([{ isIntersecting }]) => {
        if (isIntersecting) {
          // Manually trigger a refetch
          fetch()

          stop()
        }
      },
      {
        rootMargin: '100px',
      }
    )

    const loadMore = async () => {
      if (!loading.value && hasPages.value) {
        loading.value = true
        try {
          const response: PostPagination = await $axios.$get<PostPagination>(
            nextPageUrl.value
          )

          morePosts.value = [...morePosts.value, ...response.items]
          nextPageUrl.value = response.nextPageUrl
          hasPages.value = response.hasPages
        } finally {
          loading.value = false
        }
      }
    }

    return {
      target,
      loading,
      posts,
      hasPages,
      morePosts,
      loadMore,
    }
  },
})
</script>

<template>
  <div id="reviews" ref="target" class="py-4">
    <v-container>
      <div class="grid grid-cols-1 xl:grid-cols-16 gap-4 pb-8">
        <div class="col-auto xl:col-span-3">
          <!-- heading -->
          <v-heading
            :level="2"
            class="font-bold uppercase text-xl xl:text-2xl leading-6 text-h3-light dark:text-h3-dark mb-4"
          >
            <nuxt-link :to="localePath(url)">{{ subcategory }}</nuxt-link>
          </v-heading>
          <!-- heading -->
        </div>
        <!-- news -->
        <div
          class="col-auto xl:col-span-12 grid grid-cols-1 xl:grid-cols-12 gap-x-4 gap-y-4 xl:gap-y-8 place-content-stretch"
        >
          <div class="col-auto xl:col-span-12">
            <div
              class="grid grid-cols-1 xl:grid-cols-9 xl:grid-rows-3 xl:grid-flow-col-dense gap-4"
            >
              <article
                v-for="(post, index) in posts"
                :key="post.id"
                class="col-auto flex flex-col border-t-2 border-bg7-light dark:border-bg7-dark"
                :class="[
                  index === index * 4
                    ? 'xl:col-span-5 xl:row-span-3'
                    : 'xl:col-span-4',
                ]"
              >
                <nuxt-link v-if="index === index * 4" :to="localePath(post.slug)">
                  <figure v-if="post.image">
                    <v-img :src="post.image" :alt="post.caption" />
                  </figure>
                </nuxt-link>
                <div class="bg-bg2-light dark:bg-bg2-dark p-2 flex-1">
                  <v-heading
                    class="font-semibold text-h3-light dark:text-h3-dark text-base xl:text-xl leading-6 transition-colors hover:text-rose-600 dark:hover:text-rose-600"
                  >
                    <nuxt-link :to="localePath(post.slug)" class="line-clamp-2">{{ post.title }}</nuxt-link>
                  </v-heading>
                </div>
              </article>
            </div>
          </div>
          <div class="col-span-full">
            <div class="grid grid-cols-1 xl:grid-cols-12 gap-4 place-content-stretch mb-4">
              <article
                v-for="post in morePosts"
                :key="post.id"
                class="col-auto xl:col-span-3 flex flex-col border-t-2 border-bg7-light dark:border-bg7-dark"
              >
                <nuxt-link v-if="post.image" :to="localePath(post.slug)">
                  <figure>
                    <v-img :src="post.image" :alt="post.caption" />
                  </figure>
                </nuxt-link>
                <div class="bg-bg2-light dark:bg-bg2-dark p-2 flex-1">
                  <v-heading
                    class="font-semibold text-h3-light dark:text-h3-dark text-base xl:text-xl transition-colors hover:text-rose-600 dark:hover:text-rose-600"
                  >
                    <nuxt-link :to="localePath(post.slug)" class="line-clamp-3">{{ post.title }}</nuxt-link>
                  </v-heading>
                </div>
              </article>
            </div>
            <button
              v-if="hasPages && posts.length"
              type="button"
              class="font-bold rounded-2xl bg-bg7-light dark:bg-bg7-dark text-white text-xl leading-6 py-2 px-16 hover:ring-2"
              :disabled="loading"
              @click.stop="loadMore"
            >
              <font-awesome-icon :icon="['fas', 'plus']" class="mr-1" />
              {{ $t('buttons.load_more') }}
            </button>
          </div>
        </div>
        <!-- news -->
      </div>
      <div>
        <v-ads v-if="ads" :ads="ads" />
        <client-only v-else>
          <Adsense
            data-ad-client="ca-pub-3438694616169600"
            data-ad-slot="2838794797"
            data-full-width-responsive="yes"
            is-new-ads-code="yes"
            data-ad-format="rectangle"
          />
        </client-only>
      </div>
    </v-container>
  </div>
</template>
