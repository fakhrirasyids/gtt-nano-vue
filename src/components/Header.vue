<template>
  <header class="fixed inset-x-0 top-0 z-[110]">
    <div
      class="transition-all duration-300 ease-out"
      :class="scrolled ? 'bg-black shadow-[0_2px_20px_rgba(0,0,0,0.4)]' : 'bg-transparent'"
    >
      <nav class="px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20 py-4 md:py-5">
        <div class="max-w-[1280px] mx-auto flex items-center justify-between gap-4">
          <!-- Logo -->
          <button
            class="flex items-center flex-shrink-0"
            @click="emit('navigate', 'home')"
          >
            <img
              :src="imgLogo"
              alt="GTTNano"
              class="h-9 md:h-10 w-auto"
            />
          </button>

          <!-- Desktop nav -->
          <div class="hidden lg:flex items-center gap-8 xl:gap-10">
            <button
              class="text-[15px] font-medium tracking-[0.2px] whitespace-nowrap transition-colors duration-200"
              :class="currentPage === 'home' ? 'text-[#009689]' : 'text-white hover:text-white/80'"
              @click="emit('navigate', 'home')"
            >
              {{ t('nav.home') }}
            </button>

            <button
              class="text-[15px] font-medium tracking-[0.2px] whitespace-nowrap transition-colors duration-200"
              :class="currentPage === 'about' ? 'text-[#009689]' : 'text-white hover:text-white/80'"
              @click="emit('navigate', 'about')"
            >
              {{ t('nav.aboutCompany') }}
            </button>

            <!-- Product Pipeline dropdown -->
            <div class="relative" ref="pipelineRef">
              <button
                class="flex items-center gap-1.5 text-[15px] font-medium tracking-[0.2px] whitespace-nowrap transition-colors duration-200"
                :class="isPipelinePage ? 'text-[#009689]' : 'text-white hover:text-white/80'"
                @click="togglePipeline"
              >
                {{ t('nav.productPipeline') }}
                <svg
                  class="h-4 w-4 transition-transform duration-200"
                  :class="pipelineOpen ? 'rotate-180' : ''"
                  viewBox="0 0 20 20" fill="currentColor"
                >
                  <path fill-rule="evenodd" d="M5.23 7.21a.75.75 0 011.06.02L10 10.94l3.71-3.71a.75.75 0 111.06 1.06l-4.24 4.25a.75.75 0 01-1.06 0L5.21 8.29a.75.75 0 01.02-1.08z" clip-rule="evenodd" />
                </svg>
              </button>

              <!-- Dropdown -->
              <Transition name="dropdown">
                <div
                  v-if="pipelineOpen"
                  class="fixed left-1/2 top-[76px] w-[980px] max-w-[calc(100vw-2rem)] -translate-x-1/2 overflow-hidden rounded-2xl border border-black/10 bg-white shadow-[0_24px_70px_rgba(0,0,0,0.2)]"
                >
                  <div class="border-b border-black/10 px-8 py-5">
                    <p class="font-['Volkhov'] text-[23px] font-bold leading-none text-[#101828]">{{ t('header.dropdownTitle') }}</p>
                  </div>

                  <div class="grid grid-cols-4 gap-7 px-8 pb-8 pt-6">
                    <button
                      v-for="item in pipelineItems"
                      :key="item.page"
                      class="group rounded-[8px] text-left transition-transform duration-200 hover:-translate-y-1 focus:outline-none focus-visible:ring-2 focus-visible:ring-[#009689] focus-visible:ring-offset-4"
                      @click="goToPipeline(item.page)"
                    >
                      <div class="h-[126px] overflow-hidden rounded-[8px] bg-gray-100">
                        <img
                          :src="item.image"
                          :alt="item.title"
                          class="h-full w-full object-cover"
                          :class="item.imageClass"
                        />
                      </div>
                      <h3 class="mt-6 text-[16px] font-bold leading-snug text-[#101828] transition-colors group-hover:text-[#009689]">
                        {{ item.title }}
                      </h3>
                      <p class="mt-2 text-[13px] leading-[1.35] text-[#667085]">
                        <template v-for="(part, index) in item.desc" :key="index">
                          <strong v-if="part.bold" class="font-bold text-[#344054]">{{ part.text }}</strong>
                          <span v-else>{{ part.text }}</span>
                        </template>
                      </p>
                    </button>
                  </div>
                </div>
              </Transition>
            </div>

            <button
              class="text-[15px] font-medium tracking-[0.2px] whitespace-nowrap transition-colors duration-200"
              :class="currentPage === 'contact' ? 'text-[#009689]' : 'text-white hover:text-white/80'"
              @click="emit('navigate', 'contact')"
            >
              {{ t('nav.contactUs') }}
            </button>
          </div>

          <!-- Right side: language + hamburger -->
          <div class="flex items-center gap-3">
            <div class="hidden md:block">
              <LanguageDropdown theme="light" />
            </div>

            <button
              class="lg:hidden p-2 text-white"
              :aria-label="t('nav.openNav')"
              @click="drawerOpen = true"
            >
              <MenuIcon :size="24" />
            </button>
          </div>
        </div>
      </nav>
    </div>

    <!-- Mobile drawer -->
    <MobileDrawerGtt
      v-model="drawerOpen"
      :current-page="currentPage"
      :logo="imgLogo"
      @navigate="handleMobileNav"
    />
  </header>
</template>

<script setup lang="ts">
import { computed, onBeforeUnmount, onMounted, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import { Menu as MenuIcon } from 'lucide-vue-next'
import LanguageDropdown from '@/components/LanguageDropdown.vue'
import MobileDrawerGtt from '@/components/MobileDrawerGtt.vue'
import imgLogo from '@/assets/gtt/09100268d4e53aba4728250212eca777cd8fb25b.png'

import heroSlide02 from '@/assets/gtt/c0ab7a1d4dda2bd0ad42477b59706868447935b6.png'
import heroSlide03 from '@/assets/gtt/96f118309c104bbe9320c0a3eec34d6a987a4d08.png'
import heroSlide04 from '@/assets/gtt/5d65a2acd9cbca36d942b6f6bd3cd48054e18b26.jpg'
import imgNext from '@/assets/gtt/12b1ceaf647f00d1aa5ee32ec916614e30e3aa5f.png'

import type { PageName } from '@/App.vue'

const props = defineProps<{
  currentPage: PageName
}>()

const emit = defineEmits<{
  (e: 'navigate', page: PageName): void
}>()

const { t } = useI18n({ useScope: 'global' })

const scrolled = ref(false)
const drawerOpen = ref(false)
const pipelineOpen = ref(false)
const pipelineRef = ref<HTMLElement | null>(null)

const isPipelinePage = computed(() =>
  ['gttn-dx', 'gttn-navi', 'gttn-tx'].includes(props.currentPage)
)

const pipelineItems = computed(() => [
  {
    page: 'gttn-dx' as PageName,
    title: 'GTTN-Dx / GTTN-SCI',
    desc: [
      { text: t('software.cards.dx.plain') },
      { text: t('software.cards.dx.bold'), bold: true },
    ],
    image: heroSlide02,
    imageClass: 'object-left',
  },
  {
    page: 'gttn-navi' as PageName,
    title: 'GTTN-Navi',
    desc: [
      { text: t('software.cards.navi.plain') },
      { text: t('software.cards.navi.bold'), bold: true },
    ],
    image: heroSlide03,
  },
  {
    page: 'gttn-tx' as PageName,
    title: 'GTTN-Tx',
    desc: [
      { text: t('software.cards.tx.plain') },
      { text: t('software.cards.tx.bold'), bold: true },
    ],
    image: heroSlide04,
  },
  {
    page: 'home' as PageName,
    title: t('software.cards.next.title'),
    desc: [
      { text: t('software.cards.next.plain') },
      { text: t('software.cards.next.bold'), bold: true },
    ],
    image: imgNext,
  },
])

function togglePipeline() {
  pipelineOpen.value = !pipelineOpen.value
}

function goToPipeline(page: PageName) {
  pipelineOpen.value = false
  emit('navigate', page)
}

function handleMobileNav(page: PageName) {
  drawerOpen.value = false
  emit('navigate', page)
}

function onScroll() {
  scrolled.value = window.scrollY > 20
}

function onDocClick(e: MouseEvent) {
  if (pipelineRef.value && !pipelineRef.value.contains(e.target as Node)) {
    pipelineOpen.value = false
  }
}

onMounted(() => {
  onScroll()
  window.addEventListener('scroll', onScroll, { passive: true })
  document.addEventListener('click', onDocClick, { capture: true })
})

onBeforeUnmount(() => {
  window.removeEventListener('scroll', onScroll)
  document.removeEventListener('click', onDocClick, { capture: true } as any)
})
</script>

<style scoped>
.dropdown-enter-active,
.dropdown-leave-active {
  transition: opacity 0.18s ease, transform 0.18s ease;
}
.dropdown-enter-from,
.dropdown-leave-to {
  opacity: 0;
  transform: translateX(-50%) translateY(-6px);
}
.dropdown-enter-to,
.dropdown-leave-from {
  opacity: 1;
  transform: translateX(-50%) translateY(0);
}
</style>
