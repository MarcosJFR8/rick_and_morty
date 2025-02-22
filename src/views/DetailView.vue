<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { useRoute } from 'vue-router';

const route =useRoute()
const id = route.params.id
const character = ref()

const loadCharacters = async () => {
  const response = await fetch(`https://rickandmortyapi.com/api/character/${id}`)
  const data = await response.json()
  character.value = data
  console.log(character.value)
  console.log(data)
}

onMounted(() => {
    loadCharacters()
})
</script>


<!-- <template>
<div class="flex justify-center items-center h-screen">
    <div class=" grid grid-cols-1 lg:grid-cols-2 mt-8 lg:w-6xl" v-if="character">
        <div class=" mt-5 flex justify-center">
            <img class=" rounded-2xl border-6 border-blue-800" :src="character.image" :alt="character.name">
        </div>
        <div class=" flex flex-col justify-center items-center text-center mx-auto mt-8 shadow-2xl p-4 rounded-2xl w-lg h-46 lg:mt-0">
            <h1 class=" text-2xl font-semibold mb-4">Nombre: {{ character.name }}</h1>
            <p>Lugar: {{ character.location.name }}</p>
            <p>Status: {{ character.status }}</p>
            <p>Especie: {{ character.species }}</p>
            <p>Genero: {{ character.gender }}</p>
        </div>
    </div>
</div>
</template> -->

<template>
    <div class="flex justify-center items-center h-screen">
      <div class="grid grid-cols-1 lg:grid-cols-2 gap-8 lg:w-6xl" v-if="character">
        <!-- Image Container -->
        <div class="flex justify-center items-center">
          <img class="rounded-2xl border-4 border-blue-800" :src="character.image" :alt="character.name">
        </div>
  
        <!-- Description Card Container -->
        <div class="flex justify-center items-center">
          <div class="text-center p-4 shadow-2xl rounded-2xl bg-white">
            <h1 class="text-2xl font-semibold mb-4">Nombre: {{ character.name }}</h1>
            <p class="mb-2">Lugar: {{ character.location.name }}</p>
            <p class="mb-2">Status: {{ character.status }}</p>
            <p class="mb-2">Especie: {{ character.species }}</p>
            <p class="mb-2">Genero: {{ character.gender }}</p>
          </div>
        </div>
      </div>
    </div>
  </template>