<template>
  <!-- Hero -->
  <section class="relative h-[56vw] min-h-[380px] max-h-[600px] overflow-hidden bg-[#0d1b2a]">
    <img :src="heroImg" alt="GTTN-Dx hero" class="absolute inset-0 w-full h-full object-cover object-center opacity-70" />
    <div class="absolute inset-0" style="background: linear-gradient(to right, rgba(5,12,30,0.88) 0%, rgba(5,12,30,0.55) 55%, transparent 100%)" />
    <div class="relative z-10 h-full flex items-center">
      <div class="max-w-[1280px] mx-auto w-full px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20">
        <div class="max-w-[560px] pt-20">
          <h1 class="font-['Volkhov'] font-bold text-white text-[36px] sm:text-[48px] lg:text-[56px] leading-tight">
            GTTN-Dx /<br />GTTN-SCI
          </h1>
          <p class="mt-3 text-white/80 font-sans text-base sm:text-lg leading-relaxed">
            {{ t('gttnDx.heroSubtitle') }}
          </p>
          <button class="mt-6 inline-flex items-center justify-center rounded-[6px] bg-white px-6 py-3 font-semibold text-[#101828] text-sm sm:text-base hover:-translate-y-0.5 transition-transform">
            {{ t('gttnDx.contactDemo') }}
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- Section 1: Screen before Symptoms -->
  <section class="py-14 sm:py-16 lg:py-20 bg-[#f0f8ff]">
    <div class="max-w-[1280px] mx-auto px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 lg:gap-16 items-center">
        <div>
          <p class="font-sans font-semibold text-[#009689] text-sm uppercase tracking-[0.1em] mb-3">{{ t('gttnDx.screeningKicker') }}</p>
          <h2 class="font-['Volkhov'] font-bold text-[#101828] text-2xl sm:text-3xl lg:text-4xl mb-5">
            {{ t('gttnDx.screeningTitle') }}
          </h2>
          <p class="font-sans text-[#344054] text-sm sm:text-base leading-relaxed">
            {{ t('gttnDx.screeningDesc') }}
          </p>
        </div>
        <div class="rounded-2xl overflow-hidden border border-black/8 bg-white p-3 shadow-[0_16px_48px_rgba(15,23,42,0.08)]">
          <img :src="imgScreening" alt="Cancer screening visualization" class="w-full rounded-xl object-cover" />
        </div>
      </div>
    </div>
  </section>

  <!-- Section 2: CFDA Certification -->
  <section class="py-14 sm:py-16 lg:py-20 bg-[#0d1b2a]">
    <div class="max-w-[1280px] mx-auto px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20 text-center">
      <div class="inline-block rounded-full border border-white/25 px-5 py-1.5 text-white/80 text-xs font-semibold uppercase tracking-widest mb-8">
        {{ t('gttnDx.certKicker') }}
      </div>
      <h2 class="font-['Volkhov'] font-bold text-white text-2xl sm:text-3xl lg:text-4xl mb-4">
        {{ t('gttnDx.certTitle') }}
      </h2>
      <p class="font-sans text-white/65 text-sm sm:text-base max-w-2xl mx-auto leading-relaxed mb-12">
        {{ t('gttnDx.certDesc') }}
      </p>

      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 lg:gap-12 items-center text-left">
        <div class="flex justify-center">
          <div class="rounded-2xl overflow-hidden border border-white/15 bg-white/5 p-3 max-w-[280px] w-full">
            <img :src="imgCert" alt="CFDA Certificate" class="w-full rounded-xl object-cover" />
          </div>
        </div>
        <div>
          <p class="font-sans text-white/65 text-sm sm:text-base leading-relaxed">
            {{ t('gttnDx.certBody') }}
          </p>
        </div>
      </div>
    </div>
  </section>

  <!-- Section 3: Value Proposition -->
  <section class="py-14 sm:py-16 lg:py-20 bg-white">
    <div class="max-w-[1280px] mx-auto px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-10 lg:gap-16 items-center">
        <div>
          <p class="font-sans font-semibold text-[#009689] text-sm uppercase tracking-[0.1em] mb-3">{{ t('gttnDx.valueKicker') }}</p>
          <h2 class="font-['Volkhov'] font-bold text-[#101828] text-2xl sm:text-3xl lg:text-4xl mb-5 whitespace-pre-line">
            {{ t('gttnDx.valueTitle') }}
          </h2>
          <p class="font-sans text-[#344054] text-sm sm:text-base leading-relaxed mb-8">
            {{ t('gttnDx.valueDesc') }}
          </p>

          <div class="grid grid-cols-1 sm:grid-cols-3 gap-4">
            <div
              v-for="(point, index) in valuePoints"
              :key="index"
              class="flex flex-col items-center text-center p-4 rounded-2xl bg-[#f0f8ff] gap-3"
            >
              <div class="h-10 w-10 rounded-full bg-[#009689]/15 flex items-center justify-center">
                <component :is="point.icon" :size="20" class="text-[#009689]" />
              </div>
              <p class="font-sans text-xs sm:text-sm font-medium text-[#101828] leading-snug">{{ point.text }}</p>
            </div>
          </div>
        </div>
        <div class="flex justify-center">
          <div class="rounded-full overflow-hidden border border-black/8 w-[280px] h-[280px] sm:w-[320px] sm:h-[320px] shadow-[0_20px_60px_rgba(15,23,42,0.1)]">
            <img :src="imgCells" alt="Cell visualization" class="w-full h-full object-cover" />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import { Eye, Microscope, ShieldCheck } from 'lucide-vue-next'
import heroImg from '@/assets/gtt/c0ab7a1d4dda2bd0ad42477b59706868447935b6.png'
import imgScreening from '@/assets/gtt/84858028971f5af6032d388f32bd93bafb2bf1ce.png'
import imgCert from '@/assets/gtt/592af24b3ae7436288551302e2953e30443d299e.png'
import imgCells from '@/assets/gtt/9c9ace973e69ea70ca9c9ac8c5ee50d97b45ef8b.png'

const { t, tm } = useI18n({ useScope: 'global' })

const valuePoints = computed(() => {
  const points = tm('gttnDx.valuePoints') as string[]
  const icons = [Eye, Microscope, ShieldCheck]
  return points.map((text, i) => ({ text, icon: icons[i] }))
})
</script>
