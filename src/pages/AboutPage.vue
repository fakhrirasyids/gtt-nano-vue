<template>
  <section class="bg-[#001c19] text-white">
    <div class="mx-auto max-w-[1280px] px-4 pb-20 pt-36 sm:px-6 sm:pb-24 sm:pt-40 lg:px-12 lg:pb-28 xl:px-16">
      <div class="mx-auto max-w-[960px] text-center">
        <div class="inline-flex rounded-full bg-white/10 px-8 py-3 text-sm font-bold uppercase tracking-wide text-white sm:text-base">
          {{ t('aboutPage.kicker') }}
        </div>

        <h1 class="mt-9 font-['Volkhov'] text-[38px] font-bold leading-[1.12] text-white sm:text-5xl lg:text-[56px]">
          {{ t('aboutPage.title') }}
        </h1>

        <p class="mx-auto mt-7 max-w-[780px] text-base font-light leading-8 text-white/50 sm:text-xl">
          {{ t('aboutPage.subtitle') }}
        </p>
      </div>

      <div class="mx-auto mt-20 grid max-w-[880px] gap-10 rounded-[8px] bg-[#001f26] px-6 py-10 sm:px-10 md:grid-cols-2 lg:px-14 lg:py-14">
        <article>
          <h2 class="text-[28px] font-bold text-[#27bfe5] sm:text-[32px]">
            {{ t('aboutPage.mission.title') }}
          </h2>
          <p class="mt-7 text-[15px] leading-8 text-white/75 sm:text-base">
            {{ t('aboutPage.mission.body') }}
          </p>
        </article>

        <article>
          <h2 class="text-[28px] font-bold text-[#27bfe5] sm:text-[32px]">
            {{ t('aboutPage.vision.title') }}
          </h2>
          <p class="mt-7 text-[15px] leading-8 text-white/75 sm:text-base">
            {{ t('aboutPage.vision.body') }}
          </p>
        </article>
      </div>

      <div class="mt-20 text-center">
        <h2 class="font-['Volkhov'] text-4xl font-bold leading-tight text-white sm:text-5xl">
          {{ t('aboutPage.technology.title') }}
        </h2>
      </div>

      <div class="mx-auto mt-12 grid max-w-[880px] gap-8 md:grid-cols-3">
        <article
          v-for="item in technologyItems"
          :key="item.key"
          class="rounded-[8px] border border-[#17383f] bg-[#001f26] p-7 text-left sm:p-8"
        >
          <div class="flex h-12 w-12 items-center justify-center rounded-full bg-[#0aa39a] text-white">
            <component :is="item.icon" :size="24" :stroke-width="2.4" />
          </div>
          <h3 class="mt-6 text-xl font-bold leading-snug text-white sm:text-2xl">
            {{ t(`aboutPage.technology.items.${item.key}.title`) }}
          </h3>
          <p class="mt-6 text-sm leading-7 text-white/60 sm:text-[15px]">
            {{ t(`aboutPage.technology.items.${item.key}.body`) }}
          </p>
        </article>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Activity, Clock3, Layers3 } from 'lucide-vue-next'
import { useI18n } from 'vue-i18n'

const { t } = useI18n({ useScope: 'global' })

const technologyItems = [
  { key: 'precision', icon: Layers3 },
  { key: 'detection', icon: Clock3 },
  { key: 'therapy', icon: Activity },
]
</script>
