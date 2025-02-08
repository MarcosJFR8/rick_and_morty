<script setup lang="ts">
import { onMounted } from 'vue'

const loadCharacters = async () => {
  const response = await fetch('https://rickandmortyapi.com/api/character')
  const data = await response.json()
  console.log(data)
}

onMounted(() => {
  loadCharacters()
})
</script>

<template>
  <main>
    hola
  </main>
</template>
