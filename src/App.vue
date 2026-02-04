<script setup lang="ts">
import { computed, ref } from 'vue'
import { OccasionType, ToneType, type LanguageType } from './types'
import { LANGUAGES } from './constants'
import { generateGreeting } from './service/geminiService'
import AppHeader from './components/AppHeader.vue'

const occasion = ref<OccasionType>(OccasionType.BIRTHDAY)
const name = ref('')
const age = ref('')
const interests = ref('')

const tone = ref<ToneType>(ToneType.FRIENDLY)
const language = ref<LanguageType>('Русский')
const generatedText = ref<string>('')

const loading = ref<boolean>(false)
const error = ref<string | null>(null)

const tones = computed(() => Object.values(ToneType))

const handleGenerate = async (): Promise<void> => {
  if (!name.value.trim()) {
    error.value = 'Пожалуйста, введи имя адресата.'
    return
  }

  error.value = null
  loading.value = true
  generatedText.value = ''

  try {
    const result = await generateGreeting(
      occasion.value,
      name.value,
      age.value,
      interests.value,
      tone.value,
      language.value,
    )
    generatedText.value = result
  } catch (error) {
    if (error instanceof Error) {
      console.error(error)
    }
  }
}
</script>

<template>
  <div class="min-h-screen bg-[#faf5ff]">
    <AppHeader />

    <div>
      <p>{{ occasion }}</p>
      <p>{{ name }}</p>
      <p>{{ age }}</p>
      <p>{{ interests }}</p>
      <p>{{ tone }}</p>
      <p>{{ language }}</p>
      <p>{{ generatedText }}</p>
      <p>{{ error }}</p>
    </div>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8 sm:py-12">
      <div class="max-w-7xl mx-auto">
        <div>
          <button @click="occasion = OccasionType.BIRTHDAY">День Рождения</button>
          <button @click="occasion = OccasionType.NEW_YEAR">Новый Год</button>
        </div>

        <div>
          <input type="text" placeholder="Сабыржан" v-model="name" /> <br />
          <input type="number" placeholder="18" v-model="age" /> <br />
          <textarea
            rows="2"
            placeholder="Путешествие, кодинг, плаванье..."
            v-model="interests"
          ></textarea>
        </div>

        <div>
          <button v-for="t in tones" :key="t" @click="tone = t">
            {{ t }}
          </button>
        </div>

        <div>
          <select v-model="language">
            <option v-for="lang in LANGUAGES" :key="lang" :value="lang">
              {{ lang }}
            </option>
          </select>
        </div>

        <button @click="handleGenerate" :disabled="loading">СОЗДАТЬ МАГИЮ</button>
      </div>
    </main>
  </div>
</template>
