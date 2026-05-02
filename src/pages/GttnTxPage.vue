<template>
  <!-- Hero -->
  <section class="relative h-[56vw] min-h-[380px] max-h-[600px] overflow-hidden bg-[#0d1b2a]">
    <img :src="heroImg" alt="GTTN-Tx hero" class="absolute inset-0 w-full h-full object-cover object-center opacity-65" />
    <div class="absolute inset-0" style="background: linear-gradient(to right, rgba(5,12,30,0.88) 0%, rgba(5,12,30,0.55) 55%, transparent 100%)" />
    <div class="relative z-10 h-full flex items-center">
      <div class="max-w-[1280px] mx-auto w-full px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20">
        <div class="max-w-[560px] pt-20">
          <h1 class="font-['Volkhov'] font-bold text-white text-[36px] sm:text-[48px] lg:text-[56px] leading-tight">
            GTTN-Tx
          </h1>
          <p class="mt-3 text-white/80 font-sans text-base sm:text-lg leading-relaxed">
            {{ t('gttnTx.heroSubtitle') }}
          </p>
          <button class="mt-6 inline-flex items-center justify-center rounded-[6px] bg-white px-6 py-3 font-semibold text-[#101828] text-sm sm:text-base hover:-translate-y-0.5 transition-transform">
            {{ t('gttnTx.contactDemo') }}
          </button>
        </div>
      </div>
    </div>
  </section>

  <!-- Coming Soon content -->
  <section class="py-20 sm:py-28 bg-white">
    <div class="max-w-[1280px] mx-auto px-4 md:px-8 lg:px-12 xl:px-16 2xl:px-20 text-center">
      <div class="max-w-2xl mx-auto">
        <div class="inline-block rounded-full bg-[#009689]/10 text-[#009689] text-xs font-semibold uppercase tracking-widest px-5 py-1.5 mb-8">
          {{ t('gttnTx.devBadge') }}
        </div>
        <h2 class="font-['Volkhov'] font-bold text-[#101828] text-3xl sm:text-4xl lg:text-5xl mb-6">
          {{ t('gttnTx.devTitle') }}
        </h2>
        <p class="font-sans text-[#475467] text-base sm:text-lg leading-relaxed mb-10">
          {{ t('gttnTx.devDesc') }}
        </p>

        <div class="grid grid-cols-1 sm:grid-cols-3 gap-6 mb-12">
          <div
            v-for="(stat, index) in stats"
            :key="index"
            class="rounded-2xl bg-[#f8faff] border border-[#e5e7eb] p-6 text-center"
          >
            <p class="font-['Volkhov'] font-bold text-[#009689] text-3xl mb-2">{{ stat.value }}</p>
            <p class="font-sans text-[#475467] text-sm">{{ stat.label }}</p>
          </div>
        </div>

        <div class="rounded-3xl bg-[#0d1b2a] p-8 sm:p-10 text-white text-left">
          <h3 class="font-['Volkhov'] font-bold text-xl sm:text-2xl mb-4">{{ t('gttnTx.milestonesTitle') }}</h3>
          <ul class="space-y-4">
            <li v-for="(milestone, index) in milestones" :key="index" class="flex gap-4 items-start">
              <div class="h-6 w-6 rounded-full flex-shrink-0 mt-0.5"
                :class="index < 2 ? 'bg-[#009689]' : 'border-2 border-white/25'"
              >
                <svg v-if="index < 2" class="w-6 h-6 text-white" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2.5" d="M5 13l4 4L19 7" />
                </svg>
              </div>
              <div>
                <p class="font-semibold text-sm text-white">{{ milestone.label }}</p>
                <p class="text-white/55 text-xs mt-0.5">{{ milestone.desc }}</p>
              </div>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue'
import { useI18n } from 'vue-i18n'
import heroImg from '@/assets/gtt/5d65a2acd9cbca36d942b6f6bd3cd48054e18b26.jpg'

const { t, tm } = useI18n({ useScope: 'global' })

const stats = computed(() => tm('gttnTx.stats') as Array<{ value: string; label: string }>)
const milestones = computed(() => tm('gttnTx.milestones') as Array<{ label: string; desc: string }>)
</script>
