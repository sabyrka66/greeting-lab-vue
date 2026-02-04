<script setup lang="ts">
import { ref } from 'vue'
import { OccasionType } from './types'

const occasion = ref<OccasionType>(OccasionType.BIRTHDAY)

const name = ref<string>('')
const age = ref<string>('')

const interests = ref<string>('')
</script>

<template>
  <div class="min-h-screen bg-[#faf5ff]">
    <header>Генератор поздравлений</header>

    <div>
      <p>{{ occasion }}</p>

      <p>{{ name }}</p>
      <p>{{ age }}</p>

      <p>{{ interests }}</p>
    </div>

    <main class="container mx-auto px-4 sm:px-6 lg:px-8 py-8 sm:py-12">
      <div class="max-w-7xl mx-auto">
        <div>
          <button @click="occasion = OccasionType.BIRTHDAY">День Рождения</button>
          <button @click="occasion = OccasionType.NEW_YEAR">Новый Год</button>
        </div>

        <div>
          <input type="text" placeholder="Сабыржан" v-model="name" />
          <br />

          <input type="number" placeholder="18" v-model="age" />
          <br />

          <textarea
            rows="2"
            placeholder="Путешествие, кодинг, плаванье..."
            v-model="interests"
          ></textarea>
        </div>
      </div>
    </main>
  </div>
</template>
