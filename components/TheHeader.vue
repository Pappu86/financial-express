<script lang="ts">
import dayjs from 'dayjs'
import {
  defineComponent,
  ref,
  useRouter,
  watch,
  useContext,
  onMounted,
} from '@nuxtjs/composition-api'
import { useWindowScroll, useToggle } from '@vueuse/core'
import { useAdsModalStore } from '~/store/ads/modal'

export default defineComponent({
  name: 'TheHeader',

  setup() {
    // load ads
    const adsStore = useAdsModalStore()
    adsStore.getModalPageAds()
    const menus = ref([
      {
        id: 1,
        title: 'home',
        key: 'home',
        slug: '/',
      },
      {
        id: 2,
        title: 'economy',
        key: 'economy',
        slug: '/economy',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: 'bangladesh',
            key: 'bangladesh',
            slug: '/page/economy/bangladesh',
          },
          {
            id: 2,
            title: 'global',
            key: 'global',
            slug: '/page/economy/global',
          },
        ],
      },
      {
        id: 3,
        title: 'stock',
        key: 'stock',
        slug: '/stock',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: 'bangladesh',
            key: 'bangladesh',
            slug: '/page/stock/bangladesh',
          },
          {
            id: 2,
            title: 'global',
            key: 'global',
            slug: '/page/stock/global',
          },
        ],
      },
      {
        id: 4,
        title: 'trade',
        key: 'trade',
        slug: '/trade',
      },
      {
        id: 5,
        title: 'national',
        key: 'national',
        slug: '/national',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: 'politics',
            key: 'politics',
            slug: '/page/national/politics',
          },
          {
            id: 2,
            title: 'country',
            key: 'country',
            slug: '/page/national/country',
          },
          {
            id: 3,
            title: 'crime',
            key: 'crime',
            slug: '/page/national/crime',
          },
        ],
      },
      {
        id: 6,
        title: 'world',
        key: 'world',
        slug: '/world',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: 'america',
            key: 'america',
            slug: '/page/world/america',
          },
          {
            id: 2,
            title: 'asia',
            key: 'asia',
            slug: '/page/world/asia',
          },
          {
            id: 3,
            title: 'europe',
            key: 'europe',
            slug: '/page/world/europe',
          },
          {
            id: 4,
            title: 'africa',
            key: 'africa',
            slug: '/page/world/africa',
          },
        ],
      },
      {
        id: 7,
        title: 'editorial',
        key: 'editorial',
        slug: '/editorial',
      },
      {
        id: 8,
        title: 'views',
        key: 'views',
        slug: '/views',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: 'reviews',
            key: 'reviews',
            slug: '/page/views/reviews',
          },
          {
            id: 2,
            title: 'opinions',
            key: 'opinions',
            slug: '/page/views/opinions',
          },
          {
            id: 3,
            title: 'columns',
            key: 'columns',
            slug: '/page/views/columns',
          },
          {
            id: 4,
            title: 'analysis',
            key: 'analysis',
            slug: '/page/views/analysis',
          },
          {
            id: 5,
            title: 'letters',
            key: 'letters',
            slug: '/page/views/letters',
          },
          {
            id: 6,
            title: 'economic_trends_and_insights',
            key: 'economic-trends-and-insights',
            slug: '/page/views/economic-trends-and-insights',
          },
        ],
      },
      {
        id: 9,
        title: 'more',
        key: 'more',
        slug: '/',
        hasChildren: true,
        children: [
          {
            id: 22,
            title: 'education',
            key: 'education',
            slug: '/education',
            hasChildren: true,
            children: [
              {
                id: 1,
                title: 'article',
                key: 'article',
                slug: '/page/education/article',
              },
            ],
          },
          {
            id: 30,
            title: 'media',
            key: 'media',
            slug: '/media',
          },
          {
            id: 84,
            title: 'bangla',
            key: 'bangla',
            slug: '/bn',
          },
          {
            id: 23,
            title: 'sci_tech',
            key: 'sci-tech',
            slug: '/sci-tech',
          },
          {
            id: 24,
            title: 'health',
            key: 'health',
            slug: '/health',
          },
          {
            id: 25,
            title: 'sports',
            key: 'sports',
            slug: '/sports',
            hasChildren: true,
            children: [
              {
                id: 1,
                title: 'cricket',
                key: 'cricket',
                slug: '/page/sports/cricket',
              },
              {
                id: 1,
                title: 'football',
                key: 'football',
                slug: '/page/sports/football',
              },
              {
                id: 1,
                title: 'more_sports',
                key: 'more-sports',
                slug: '/page/sports/more-sports',
              },
            ],
          },
          {
            id: 26,
            title: 'lifestyle',
            key: 'lifestyle',
            slug: '/lifestyle',
            hasChildren: true,
            children: [
              {
                id: 1,
                title: 'living',
                key: 'living',
                slug: '/page/lifestyle/living',
              },
              {
                id: 2,
                title: 'entertainment',
                key: 'entertainment',
                slug: '/page/lifestyle/entertainment',
              },
              {
                id: 3,
                title: 'food',
                key: 'food',
                slug: '/page/lifestyle/food',
              },
              {
                id: 4,
                title: 'culture',
                key: 'culture',
                slug: '/page/lifestyle/culture',
              },
              {
                id: 5,
                title: 'others',
                key: 'others',
                slug: '/page/lifestyle/others',
              },
              // {
              //   id: 6,
              //   title: 'gallery',
              //   key: 'gallery',
              //   slug: '/page/lifestyle/gallery',
              // },
            ],
          },
          {
            id: 41,
            title: 'environment',
            key: 'environment',
            slug: '/environment',
          },
          {
            id: 42,
            title: 'jobs_and_opportunities',
            key: 'jobs-and-opportunities',
            slug: '/jobs-and-opportunities',
          },
          // {
          //   id: 30,
          //   title: 'others',
          //   key: 'others',
          //   slug: '/others',
          // },
          {
            id: 27,
            title: 'youth_and_entrepreneurs',
            key: 'youth-and-entrepreneurship',
            slug: '/youth-and-entrepreneurship',
            hasChildren: true,
            children: [
              // {
              //   id: 65,
              //   title: 'youth',
              //   key: 'youth',
              //   slug: '/page/youth-and-entrepreneurship/youth',
              // },
              // {
              //   id: 66,
              //   title: 'entrepreneurship',
              //   key: 'entrepreneurship',
              //   slug: '/page/youth-and-entrepreneurship/entrepreneurship',
              // },
              {
                id: 67,
                title: 'startups',
                key: 'startups',
                slug: '/page/youth-and-entrepreneurship/startups',
              },
            ],
          },
          // {
          //   id: 28,
          //   title: 'personal_finance',
          //   key: 'personal-finance',
          //   slug: '/personal-finance',
          //   hasChildren: true,
          //   children: [
          //     {
          //       id: 69,
          //       title: 'tax',
          //       key: 'tax',
          //       slug: '/page/personal-finance/tax',
          //     },
          //     {
          //       id: 70,
          //       title: 'borrow',
          //       key: 'borrow',
          //       slug: '/page/personal-finance/borrow',
          //     },
          //     {
          //       id: 71,
          //       title: 'mutual_funds',
          //       key: 'mutual-funds',
          //       slug: '/page/personal-finance/mutual-funds',
          //     },
          //     {
          //       id: 72,
          //       title: 'save',
          //       key: 'save',
          //       slug: '/page/personal-finance/save',
          //     },
          //     {
          //       id: 73,
          //       title: 'news',
          //       key: 'news',
          //       slug: '/page/personal-finance/news',
          //     },
          //     {
          //       id: 74,
          //       title: 'spend',
          //       key: 'spend',
          //       slug: '/page/personal-finance/spend',
          //     },
          //     {
          //       id: 75,
          //       title: 'calculators',
          //       key: 'calculators',
          //       slug: '/page/personal-finance/calculators',
          //     },
          //     {
          //       id: 76,
          //       title: 'invest',
          //       key: 'invest',
          //       slug: '/page/personal-finance/invest',
          //     },
          //   ],
          // },
          // {
          //   id: 31,
          //   title: 'special_issues',
          //   key: 'special-issues',
          //   slug: '/special-issues',
          //   hasChildren: true,
          //   children: [
          //     {
          //       id: 42,
          //       title: 'power_energy',
          //       key: 'power-energy',
          //       slug: '/page/special-issues/power-energy',
          //     },
          //     {
          //       id: 43,
          //       title: 'rmg_textile',
          //       key: 'rmg-textile',
          //       slug: '/page/special-issues/rmg-textile',
          //     },
          //     {
          //       id: 44,
          //       title: 'power_energy_2',
          //       key: 'power-energy-2',
          //       slug: '/page/special-issues/power-energy-2',
          //     },
          //     {
          //       id: 45,
          //       title: 'rmg_textile_4',
          //       key: 'rmg-textile-4',
          //       slug: '/page/special-issues/rmg-textile-4',
          //     },
          //     {
          //       id: 46,
          //       title: 'rmg_textile_5',
          //       key: 'rmg-textile-5',
          //       slug: '/page/special-issues/rmg-textile-5',
          //     },
          //     {
          //       id: 48,
          //       title: 'special_on_independence_day',
          //       key: 'special-on-independence-day',
          //       slug: '/page/special-issues/special-on-independence-day',
          //     },
          //     {
          //       id: 49,
          //       title: 'pahela_baishakh_1425',
          //       key: 'pahela-baishakh-1425',
          //       slug: '/page/special-issues/pahela-baishakh-1425',
          //     },
          //     {
          //       id: 51,
          //       title: 'special_on_national_mourning_day',
          //       key: 'special-on-national-mourning-day',
          //       slug: '/page/special-issues/special-on-national-mourning-day',
          //     },
          //   ],
          // },
        ],
      },
    ])

    const publicationMenu = ref([
      {
        id: 1,
        title: '31st_year_of_publication',
        key: '31st_year_of_publication',
        slug: '#',
        hasChildren: true,
        children: [
          {
            id: 1,
            title: '30th_anniversary_issue_1',
            key: '30th-anniversary-issue-1',
            slug: 'https://today.thefinancialexpress.com.bd/30th-anniversary-issue-1',
          },
          {
            id: 2,
            title: '30th_anniversary_issue_2',
            key: '30th-anniversary-issue-2',
            slug: 'https://today.thefinancialexpress.com.bd/30th-anniversary-issue-2',
          },
          {
            id: 3,
            title: '30th_anniversary_issue_3',
            key: '30th-anniversary-issue-3',
            slug: 'https://today.thefinancialexpress.com.bd/30th-anniversary-issue-3',
          },
        ],
      },
    ])

    function openMenu(menu: any, index: number) {
      menu.showChildren = true
      menus.value.splice(index, 1, menu)
    }
    function closeMenu(menu: any, index: number) {
      menu.showChildren = false
      menus.value.splice(index, 1, menu)
    }

    function getMenuStr(title: any) {
      return 'menus.' + title
    }

    const target = ref<HTMLElement>()
    const stickyHeader = ref<HTMLElement>()
    const { y } = useWindowScroll()
    let windowWidth = 0
    if (process.browser) {
      windowWidth = window.innerWidth
    }

    watch(y, () => {
      if (windowWidth < 1024) {
        // For mobile sticky header
        const stickyBottom =
          (stickyHeader.value?.clientHeight || 0) +
          (stickyHeader.value?.offsetTop || 0)

        if (stickyBottom - y.value <= 0) {
          stickyHeader.value?.classList.add(
            'fixed',
            'top-0',
            'left-0',
            'shadow-lg'
          )
        } else {
          stickyHeader.value?.classList.remove(
            'fixed',
            'top-0',
            'left-0',
            'shadow-lg'
          )
        }
      } else {
        // For desktop sticky menu
        const targetBottom =
          (target.value?.clientHeight || 0) + (target.value?.offsetTop || 0)

        if (targetBottom - y.value <= 0) {
          target.value?.classList.add('fixed', 'top-0', 'shadow-lg')
        } else {
          target.value?.classList.remove('fixed', 'top-0', 'shadow-lg')
        }
      }
    })

    const isSearchVisible = ref(false)
    const toggleSearch = useToggle(isSearchVisible)

    const { i18n } = useContext()
    const lang = i18n?.locale === 'bangla' ? 'bn' : 'en'
    let url = `${lang}/search`

    if (lang === 'en') {
      url = '/search'
    }

    const router = useRouter()
    const query = ref('')
    const search = () => {
      if (query.value.length) {
        router.push({
          path: url,
          query: {
            q: query.value,
            page: '1',
            per_page: '10',
            sort_by: 'desc',
          },
        })
      }
    }
    router.afterEach(() => {
      isSearchVisible.value = false
      query.value = ''
    })

    // Set search placeholder
    // setTimeout(function () {
    //   if (process.browser) {
    //     const searchElement = document.getElementById('gsc-i-id1')
    //     if (searchElement) {
    //       searchElement.setAttribute('placeholder', 'Search here...')
    //     }
    //   }
    // }, 5000)

    // Popup ads show
    const isCenterModalAds = ref(false)
    const modalAd = ref()
    onMounted(() => {
      setTimeout(function () {
        const centerModalAds = adsStore.centerModalAds
        if (centerModalAds && centerModalAds.isModal) {
          modalAd.value = centerModalAds
          isCenterModalAds.value = true
        }
      }, 2000)
    })

    return {
      target,
      stickyHeader,
      menus,
      openMenu,
      closeMenu,
      getMenuStr,
      isSearchVisible,
      toggleSearch,
      query,
      search,
      windowWidth,
      toDate: dayjs().format('dddd, D MMMM YYYY'),
      isCenterModalAds,
      modalAd,
      publicationMenu,
    }
  },
  methods: {
    closeSearch() {
      this.isSearchVisible = false
    },
    toggleModal(value: any) {
      this.isCenterModalAds = value
    },
  },
})
</script>

<template>
  <header ref="stickyHeader" class="z-50 transition-all w-full">
    <v-container>
      <div class="grid grid-cols-3 py-4 items-center">
        <div class="flex items-center">
          <button
            v-b-toggle.sidebar
            type="button"
            class="py-2 pr-2 cursor-pointer justify-self-start sm:pr-3"
          >
            <svg
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 10 8"
              class="text-gray-500 dark:text-white w-5 h-5 xl:w-7 xl:h-7"
            >
              <path
                class="block dark:hidden"
                d="M1 1h8M1 4h 10M1 7h7"
                stroke="rgb(107, 114, 128)"
                stroke-width="1"
                stroke-linecap="round"
                fill="currentColor"
              />
              <path
                class="hidden dark:block"
                d="M1 1h8M1 4h 10M1 7h7"
                stroke="rgb(255, 255, 255)"
                stroke-width="1"
                stroke-linecap="round"
                fill="currentColor"
              />
            </svg>
          </button>
          <v-theme-switch />
          <button
            type="button"
            class="py-2 cursor-pointer justify-self-end sm:px-2"
            @click="toggleSearch"
          >
            <svg
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 320 512"
              class="text-gray-500 dark:text-white w-5 h-5 xl:w-7 xl:h-7 inline-block overflow-visible"
            >
              <path
                fill="currentColor"
                d="M505 442.7L405.3 343c-4.5-4.5-10.6-7-17-7H372c27.6-35.3 44-79.7 44-128C416 93.1 322.9 0 208 0S0 93.1 0 208s93.1 208 208 208c48.3 0 92.7-16.4 128-44v16.3c0 6.4 2.5 12.5 7 17l99.7 99.7c9.4 9.4 24.6 9.4 33.9 0l28.3-28.3c9.4-9.4 9.4-24.6.1-34zM208 336c-70.7 0-128-57.2-128-128 0-70.7 57.2-128 128-128 70.7 0 128 57.2 128 128 0 70.7-57.2 128-128 128z"
              />
            </svg>
          </button>
          <language-toggle-button class="hidden sm:block" />
        </div>
        <div class="logo justify-self-center w-[13rem] sm:w-[16rem] xl:w-[20rem]">
          <router-link :to="localePath('index')">
            <picture class="hidden dark:block">
              <source media="(min-width: 1536px)" srcset="~/assets/images/logo-d-d.png" />
              <source media="(min-width: 1280px)" srcset="~/assets/images/logo-d-m-d.png" />
              <source media="(min-width: 768px)" srcset="~/assets/images/logo-t-d.png" />
              <source media="(max-width: 640px)" srcset="~/assets/images/logo-m-d.png" />
              <img src="~/assets/images/logo-m-d.png" alt="The Financial Express" />
            </picture>
            <picture class="dark:hidden">
              <source media="(min-width: 1536px)" srcset="~/assets/images/logo-d-l.png" />
              <source media="(min-width: 1280px)" srcset="~/assets/images/logo-d-m-l.png" />
              <source media="(min-width: 768px)" srcset="~/assets/images/logo-t-l.png" />
              <source media="(max-width: 640px)" srcset="~/assets/images/logo-m-l.png" />
              <img src="~/assets/images/logo-m-l.png" alt="The Financial Express" />
            </picture>
          </router-link>
          <!-- Center today date-->
          <div
            class="text-rose-600 font-bold text-xs md:text-base text-center lg:hidden xl:hidden"
          >{{ getFullDate('', $i18n.locale) }}</div>
          <!-- Center today date-->
        </div>
        <div class="flex justify-end items-center px-2">
          <a
            href="https://today.thefinancialexpress.com.bd/archive"
            class="hidden pr-2 uppercase font-bold text-rose-600 hover:text-rose-900 transition-colors text-base md:block"
          >{{ $t('buttons.archive') }}</a>
          <span class="hidden text-rose-600 font-bold text-base lg:block">
            <span class="pr-2">|</span>
            {{ getFullDate('', $i18n.locale) }}
          </span>
          <language-toggle-button class="min-lang-toggle sm:hidden" />
        </div>
        <!-- <div class="flex justify-end items-center">
          <v-theme-switch />
          <button
            type="button"
            class="px-2 py-2 cursor-pointer justify-self-end"
            @click="toggleSearch"
          >
            <svg
              role="img"
              xmlns="http://www.w3.org/2000/svg"
              viewBox="0 0 320 512"
              class="text-gray-500 dark:text-white w-5 h-5 xl:w-10 xl:h-10 inline-block overflow-visible"
            >
              <path
                fill="currentColor"
                d="M505 442.7L405.3 343c-4.5-4.5-10.6-7-17-7H372c27.6-35.3 44-79.7 44-128C416 93.1 322.9 0 208 0S0 93.1 0 208s93.1 208 208 208c48.3 0 92.7-16.4 128-44v16.3c0 6.4 2.5 12.5 7 17l99.7 99.7c9.4 9.4 24.6 9.4 33.9 0l28.3-28.3c9.4-9.4 9.4-24.6.1-34zM208 336c-70.7 0-128-57.2-128-128 0-70.7 57.2-128 128-128 70.7 0 128 57.2 128 128 0 70.7-57.2 128-128 128z"
              />
            </svg>
          </button>
        </div>-->
      </div>
    </v-container>
    <v-slide-up-down :active="!!isSearchVisible" :duration="500">
      <div class="bg-search-light dark:bg-search-dark py-3">
        <v-container>
          <div class="justify-center">
            <div class="grid grid-cols-5 gap-0 max-w-6xl mx-auto">
              <div class="col-span-4">
                <label for="search" class="sr-only">{{ $t('search') }}</label>
                <input
                  id="search"
                  v-model="query"
                  type="search"
                  name="query"
                  autocomplete="search"
                  class="focus:ring-gray focus:border-gray border-gray-600 rounded-md w-full text-base bg-bg1-light dark:bg-bg1-dark"
                  placeholder="Search here..."
                  @keyup.enter="search"
                />

                <!-- <script async src="https://cse.google.com/cse.js?cx=3432ec95775964de5"></script>
                <div class="gcse-searchbox-only"></div>-->
              </div>
              <div class="col-span-1 flex items-center">
                <button
                  class="text-base p-2 text-center text-gray dark:text-white"
                  @click.prevent="closeSearch"
                >
                  <svg
                    xmlns="http://www.w3.org/2000/svg"
                    width="17.834"
                    height="17.833"
                    viewBox="0 0 17.834 17.833"
                    class="fill-current"
                  >
                    <g
                      id="Group_763"
                      data-name="Group 763"
                      transform="translate(-1079.443 -227.443)"
                    >
                      <rect
                        id="Rectangle_107"
                        data-name="Rectangle 107"
                        width="22.927"
                        height="2.293"
                        rx="1.146"
                        transform="translate(1081.064 227.443) rotate(45)"
                      />
                      <rect
                        id="Rectangle_108"
                        data-name="Rectangle 108"
                        width="22.927"
                        height="2.292"
                        rx="1.146"
                        transform="translate(1097.277 229.064) rotate(135)"
                      />
                    </g>
                  </svg>
                </button>
              </div>
            </div>
          </div>
        </v-container>
      </div>
    </v-slide-up-down>
    <div
      ref="target"
      class="bg-menu-light dark:bg-menu-dark w-full z-50 transition-all hidden xl:block"
    >
      <v-container>
        <nav class="flex items-center justify-center">
          <div class="hidden xl:inline-grid grid-flow-col gap-x-3 xl:gap-x-2 mr-3">
            <template v-for="menu in menus">
              <div
                v-if="menu.hasChildren"
                :key="'menu_' + menu.id"
                class="group inline-block relative"
              >
                <router-link
                  class="px-1 2xl:px-2 py-3 uppercase text-menu-color-light dark:text-menu-color-dark text-base 2xl:text-xl font-bold transition-colors hover:text-red-600 hover:dark:text-white focus:text-red-600 focus:dark:text-white inline-flex justify-center items-center w-full"
                  :to="localePath(menu.slug)"
                >
                  <span class="mr-1">{{ $t(`menus.${menu.title}`) }}</span>
                  <svg
                    class="fill-current h-6 w-6 font-bold"
                    xmlns="http://www.w3.org/2000/svg"
                    viewBox="0 0 20 20"
                  >
                    <path
                      d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                    />
                  </svg>
                </router-link>
                <ul
                  class="absolute hidden pt-1 w-56 group-hover:block bg-bg2-light dark:bg-bg2-dark text-menu-color-light dark:text-menu-color-dark rounded-md outline-none z-50"
                >
                  <template v-for="child in menu.children">
                    <li
                      v-if="child.hasChildren"
                      :key="'child_' + child.key + '_' + child.id"
                      class="ml-2 mr-2 submenu"
                    >
                      <router-link
                        :to="localePath(child.slug)"
                        class="flex inline-block rounded-md w-full px-2 py-2 text-base 2xl:text-xl leading-tight text-menu-color-light dark:text-menu-color-dark hover:text-red-600 hover:dark:text-white uppercase outline-none"
                      >
                        <span class="grow">{{ $t(getMenuStr(child.title)) }}</span>
                        <span class="flex-none w-4">
                          <svg
                            class="fill-current h-6 w-6 font-bold"
                            xmlns="http://www.w3.org/2000/svg"
                            viewBox="0 0 20 20"
                          >
                            <path
                              d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                            />
                          </svg>
                        </span>
                      </router-link>
                      <hr class="border-bg5-light dark:border-bg5-dark" />
                      <ul
                        :class="'menu-' + child.key"
                        class="absolute pt-1 w-[12.5rem] inner-submenu bg-bg2-light dark:bg-bg2-dark text-menu-color-light dark:text-menu-color-dark rounded-md outline-none z-50"
                      >
                        <li
                          v-for="subChild in child.children"
                          :key="'sub_child_' + subChild.key + '_' + subChild.id"
                          class="ml-2 mr-2"
                        >
                          <router-link
                            :to="localePath(subChild.slug)"
                            class="inline-block rounded-md w-full px-2 py-2 text-base 2xl:text-xl leading-tight text-menu-color-light dark:text-menu-color-dark hover:text-red-600 hover:dark:text-white uppercase outline-none"
                          >{{ $t(getMenuStr(subChild.title)) }}</router-link>
                          <hr class="border-bg5-light dark:border-bg5-dark" />
                        </li>
                      </ul>
                    </li>
                    <li v-else :key="'child_' + child.key" class="ml-2 mr-2">
                      <router-link
                        :to="localePath(child.slug)"
                        class="inline-block rounded-md w-full px-2 py-2 text-base 2xl:text-xl leading-tight text-menu-color-light dark:text-menu-color-dark hover:text-red-600 hover:dark:text-white uppercase outline-none"
                      >{{ $t(getMenuStr(child.title)) }}</router-link>
                      <hr class="border-bg5-light dark:border-bg5-dark" />
                    </li>
                  </template>
                </ul>
              </div>
              <div v-else :key="'main_menu_' + menu.id">
                <router-link
                  class="px-1 2xl:px-2 py-3 uppercase text-menu-color-light dark:text-menu-color-dark text-base 2xl:text-xl font-bold transition-colors hover:text-red-600 hover:dark:text-white focus:text-red-600 focus:dark:text-white inline-flex justify-center items-center w-full"
                  :to="localePath(menu.slug)"
                >{{ $t(getMenuStr(menu.title)) }}</router-link>
              </div>
            </template>
          </div>
          <ul ref="target" class="m-0 p-0 inline-grid grid-flow-col gap-x-4 2xl:gap-x-8">
            <li>
              <a
                href="https://today.thefinancialexpress.com.bd"
                target="_blank"
                rel="noopener"
                class="py-1.5 uppercase text-gray dark:text-white text-xs md:text-xs xl:text-xs 2xl:text-lg font-semibold transition-colors dark:ring-white"
              >{{ $t('buttons.fe_today') }}</a>
            </li>
            <li>
              <a
                href="https://epaper.thefinancialexpress.com.bd"
                target="_blank"
                rel="noopener"
                class="py-1 uppercase text-gray dark:text-white text-xs md:text-xs xl:text-xs 2xl:text-lg font-semibold transition-colors dark:ring-white"
              >{{ $t('buttons.fe_e_paper') }}</a>
            </li>
            <!-- <li>
              <a
                href="https://today.thefinancialexpress.com.bd/budget-2023-24"
                target="_blank"
                rel="noopener"
                class="py-1 uppercase text-rose-600 hover:text-rose-900 text-xs md:text-xs xl:text-xs 2xl:text-lg font-semibold transition-colors dark:ring-white"
              >{{ $t('buttons.budget_2023_24') }}</a>
            </li>-->
          </ul>
          <template v-for="menuItem in publicationMenu">
            <div
              v-if="menuItem.hasChildren"
              :key="'menu_' + menuItem.id"
              class="group inline-block relative ml-2"
            >
              <router-link
                class="pt-1 uppercase text-rose-600 hover:text-rose-900 text-xs 2xl:text-lg font-semibold transition-colors dark:ring-white inline-flex justify-center items-center w-full"
                to="#"
              >
                <span v-html="$t(`menus.${menuItem.title}`)"></span>
                <svg
                  class="fill-current h-6 w-5 font-bold"
                  xmlns="http://www.w3.org/2000/svg"
                  viewBox="0 0 20 20"
                >
                  <path
                    d="M9.293 12.95l.707.707L15.657 8l-1.414-1.414L10 10.828 5.757 6.586 4.343 8z"
                  />
                </svg>
              </router-link>
              <ul
                class="absolute hidden pt-1 w-56 group-hover:block bg-bg2-light dark:bg-bg2-dark text-menu-color-light dark:text-menu-color-dark rounded-md outline-none z-50"
              >
                <li
                  v-for="child in menuItem.children"
                  :key="'pub_child_' + child.key"
                  class="ml-2 mr-2"
                >
                  <a
                    :href="child.slug"
                    target="_blank"
                    class="inline-block rounded-md w-full px-2 py-2 text-xs 2xl:text-lg leading-tight text-menu-color-light dark:text-menu-color-dark hover:text-red-600 hover:dark:text-white uppercase outline-none"
                    rel="author"
                    v-html="$t(getMenuStr(child.title))"
                  ></a>
                  <hr class="border-bg5-light dark:border-bg5-dark" />
                </li>
              </ul>
            </div>
          </template>
        </nav>
      </v-container>
    </div>
    <!--- Start center modal ad --->
    <div v-if="isCenterModalAds">
      <v-modal-ads v-if="modalAd" :ads="modalAd" @toggleModal="toggleModal" />
    </div>
    <!--- End center modal ad --->
  </header>
</template>

<style scoped>
/* .group ul {
  border: 3px solid #927a63;
} */
.inner-submenu {
  right: 80px;
  margin-top: -38px;
}

li > ul {
  transform: translatex(100%) scale(0);
}

li:hover > ul {
  transform: translatex(101%) scale(1);
}

li:hover > ul.menu-special-issues {
  bottom: 0;
}

li:hover > ul.menu-personal-finance {
  margin-top: -100px;
}

.scale-0 {
  transform: scale(0);
}
</style>
