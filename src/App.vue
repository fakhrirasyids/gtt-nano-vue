<template>
  <div class="min-h-screen" :class="currentPage === 'about' || currentPage === 'contact' ? 'bg-[#001c19]' : 'bg-white'">
    <Header
      :current-page="currentPage"
      @navigate="navigateTo"
    />

    <main>
      <template v-if="currentPage === 'home'">
        <HeroSection @navigate="navigateTo" />
        <ProblemSection />
        <ImageShowcaseSection />
        <HardwareSection />
        <BenefitsSection />
        <OneHealthSection />
        <SoftwareSection @navigate="navigateTo" />
        <CtaSection />
        <ContactSection />
      </template>

      <template v-else-if="currentPage === 'gttn-dx'">
        <GttnDxPage />
        <ContactSection />
      </template>

      <template v-else-if="currentPage === 'gttn-navi'">
        <GttnNaviPage />
        <ContactSection />
      </template>

      <template v-else-if="currentPage === 'gttn-tx'">
        <GttnTxPage />
        <ContactSection />
      </template>

      <template v-else-if="currentPage === 'about'">
        <AboutPage />
        <ContactSection />
      </template>

      <template v-else-if="currentPage === 'contact'">
        <ContactPage />
      </template>
    </main>
  </div>
</template>

<script setup lang="ts">
import { onBeforeUnmount, onMounted, ref, watch } from 'vue'
import Header from '@/components/Header.vue'
import HeroSection from '@/sections/HeroSection.vue'
import ProblemSection from '@/sections/ProblemSection.vue'
import ImageShowcaseSection from '@/sections/ImageShowcaseSection.vue'
import HardwareSection from '@/sections/HardwareSection.vue'
import BenefitsSection from '@/sections/BenefitsSection.vue'
import OneHealthSection from '@/sections/OneHealthSection.vue'
import SoftwareSection from '@/sections/SoftwareSection.vue'
import CtaSection from '@/sections/CtaSection.vue'
import ContactSection from '@/sections/ContactSection.vue'
import GttnDxPage from '@/pages/GttnDxPage.vue'
import GttnNaviPage from '@/pages/GttnNaviPage.vue'
import GttnTxPage from '@/pages/GttnTxPage.vue'
import AboutPage from '@/pages/AboutPage.vue'
import ContactPage from '@/pages/ContactPage.vue'

export type PageName = 'home' | 'about' | 'gttn-dx' | 'gttn-navi' | 'gttn-tx' | 'contact'

const pageNames: PageName[] = ['home', 'about', 'gttn-dx', 'gttn-navi', 'gttn-tx', 'contact']

function pageFromHash(): PageName {
  const hash = window.location.hash.replace('#', '') as PageName
  return pageNames.includes(hash) ? hash : 'home'
}

const currentPage = ref<PageName>(pageFromHash())

function navigateTo(page: PageName) {
  if (window.location.hash !== `#${page}`) {
    window.location.hash = page
  }

  currentPage.value = page
  window.scrollTo({ top: 0, behavior: 'smooth' })
}

watch(currentPage, () => {
  window.scrollTo({ top: 0 })
})

function syncPageFromHash() {
  currentPage.value = pageFromHash()
}

onMounted(() => {
  window.addEventListener('hashchange', syncPageFromHash)
})

onBeforeUnmount(() => {
  window.removeEventListener('hashchange', syncPageFromHash)
})
</script>
