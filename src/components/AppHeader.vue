<script setup lang="ts">
import { PartyPopper } from 'lucide-vue-next'
</script>

<template>
  <header className="bg-white/80 backdrop-blur-md sticky top-0 z-50 border-b border-emerald-100">
    <div className="max-w-7xl mx-auto px-4 sm:px-6 h-16 flex items-center gap-2 text-gray-800">
      <div className="bg-emerald-100 p-2 rounded-lg">
        <PartyPopper className="w-6 h-6 text-emerald-600" />
      </div>
      <h1 className="text-xl font-bold">Генератор Поздравлений</h1>
    </div>
  </header>
</template>
