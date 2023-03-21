<script setup lang="ts">
import {computed, ref} from "vue";

const input = ref(5)

const result = computed(() => {
  if (input.value < 1 || input.value > 100) {
    return 'Nur Werte zwischen 1 und 100, bitte (:'
  }

  return fibonacci(input.value)
})

function fibonacci (limit: number): number[] {
  if (limit <= 1) {
    return [limit]
  }

  const prev = fibonacci(limit - 1)

  return [
      ...prev,
      prev[prev.length - 1] + (prev.length > 1 ? prev[prev.length - 2] : 1)
  ]
}
</script>

<template>
  <div class="w-full h-full">
    <h1 class="m-4 mb-10 text-2xl font-extrabold leading-none tracking-tight text-gray-900 md:text-5xl lg:text-6xl">
      Fibonacci Zahlen
    </h1>
    <div class="m-4">
      <label for="input" class="block mb-2 text-sm font-medium text-gray-900">
        Die ersten N fibonacci-Zahlen:
      </label>
      <input v-model="input" id="input" type="number" class="border text-sm focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5">
    </div>
    <div class="m-4">
      <span v-if="Array.isArray(result)" class="block mb-2 text-sm font-medium text-gray-900">
        Ergebnis:<br>
        {{ result.join(', ') }}
      </span>
      <span v-else class="text-red-500">
        {{ result }}
      </span>
    </div>
  </div>
</template>

<style scoped></style>
