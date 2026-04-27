<template>
  <section class="min-h-screen bg-[#001c19] text-white">
    <div class="mx-auto max-w-[1280px] px-4 pb-20 pt-32 sm:px-6 sm:pb-24 sm:pt-32 lg:px-12 xl:px-16">
      <div class="mx-auto max-w-[1040px] text-center">
        <div class="inline-flex rounded-full bg-white/10 px-8 py-3 text-sm font-bold uppercase tracking-wide text-white sm:text-base">
          {{ t('contactPage.kicker') }}
        </div>

        <h1 class="mt-9 font-['Volkhov'] text-[38px] font-bold leading-[1.12] text-white sm:text-5xl lg:text-[56px]">
          {{ t('contactPage.title') }}
        </h1>

        <p class="mx-auto mt-7 max-w-[820px] text-base font-light leading-8 text-white/55 sm:text-xl">
          {{ t('contactPage.subtitle') }}
        </p>
      </div>

      <div class="mx-auto mt-16 grid max-w-[860px] gap-10 lg:grid-cols-[260px_minmax(0,1fr)] lg:gap-16">
        <aside>
          <h2 class="text-3xl font-bold leading-tight text-white sm:text-[34px]">
            {{ t('contactPage.info.title') }}
          </h2>

          <div class="mt-9 space-y-7">
            <div
              v-for="item in contactInfo"
              :key="item.key"
              class="grid grid-cols-[44px_minmax(0,1fr)] gap-4"
            >
              <div class="flex h-11 w-11 items-center justify-center rounded-full bg-[#0aa39a] text-white">
                <component :is="item.icon" :size="21" :stroke-width="2.4" />
              </div>
              <div>
                <h3 class="text-base font-semibold text-white sm:text-lg">
                  {{ t(`contactPage.info.${item.key}.label`) }}
                </h3>
                <p class="mt-1 whitespace-pre-line text-sm leading-6 text-white/55 sm:text-[15px]">
                  {{ t(`contactPage.info.${item.key}.value`) }}
                </p>
              </div>
            </div>
          </div>
        </aside>

        <form class="rounded-[8px] bg-[#001f26] px-6 py-9 sm:px-10 lg:px-12" @submit.prevent>
          <h2 class="text-3xl font-bold leading-tight text-white sm:text-[34px]">
            {{ t('contactPage.form.title') }}
          </h2>

          <div class="mt-8 grid gap-5 sm:grid-cols-2">
            <label class="block">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.fullName') }}</span>
              <input class="field mt-3" type="text" :placeholder="t('contactPage.form.placeholders.fullName')" />
            </label>

            <label class="block">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.email') }}</span>
              <input class="field mt-3" type="email" :placeholder="t('contactPage.form.placeholders.email')" />
            </label>

            <label class="block">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.company') }}</span>
              <input class="field mt-3" type="text" :placeholder="t('contactPage.form.placeholders.company')" />
            </label>

            <label class="block">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.phone') }}</span>
              <input class="field mt-3" type="tel" :placeholder="t('contactPage.form.placeholders.phone')" />
            </label>

            <label class="block sm:col-span-2">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.subject') }}</span>
              <input class="field mt-3" type="text" />
            </label>

            <label class="block sm:col-span-2">
              <span class="text-sm font-medium text-white">{{ t('contactPage.form.message') }}</span>
              <textarea class="field field-message mt-3 resize-y py-4" :placeholder="t('contactPage.form.placeholders.message')" />
            </label>
          </div>

          <button
            type="submit"
            class="mt-8 inline-flex w-full items-center justify-center gap-3 rounded-[8px] bg-[#0aa39a] px-6 py-4 text-lg font-bold text-white transition-colors hover:bg-[#0bb2a8] focus:outline-none focus:ring-2 focus:ring-[#27bfe5] focus:ring-offset-2 focus:ring-offset-[#001f26]"
          >
            <Send :size="22" :stroke-width="2.3" />
            {{ t('contactPage.form.submit') }}
          </button>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Mail, MapPin, Phone, Send } from 'lucide-vue-next'
import { useI18n } from 'vue-i18n'

const { t } = useI18n({ useScope: 'global' })

const contactInfo = [
  { key: 'email', icon: Mail },
  { key: 'phone', icon: Phone },
  { key: 'address', icon: MapPin },
]
</script>

<style scoped>
.field {
  min-height: 48px;
  width: 100%;
  border-radius: 8px;
  border: 1px solid rgba(39, 191, 229, 0.18);
  background: rgba(0, 28, 25, 0.72);
  padding: 0 1rem;
  color: white;
  font: inherit;
  outline: none;
  transition: border-color 160ms ease, box-shadow 160ms ease, background 160ms ease;
}

.field::placeholder {
  color: rgba(255, 255, 255, 0.35);
}

.field:focus {
  border-color: rgba(39, 191, 229, 0.72);
  box-shadow: 0 0 0 3px rgba(39, 191, 229, 0.12);
  background: rgba(0, 28, 25, 0.94);
}

.field-message {
  min-height: 150px;
}
</style>
