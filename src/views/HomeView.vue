<script setup lang="ts">
import { onMounted, ref } from 'vue'
import { useRouter } from 'vue-router'

const characters = ref([])
const page:any = ref(1)
const router = useRouter()

const loadCharacters = async () => {
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}`)
  const data = await response.json()
  characters.value = data.results
}

const incrementPage = () => {
  page.value++
  loadCharacters()
}

const decrementPage = () => {
  if (page.value > 1) {
    page.value--
    loadCharacters()
  }
}

const seeCharacterDetails =(character_id: number)=>{
  router.push(`details/${character_id}`)
}

onMounted(() => {
  loadCharacters()
})
</script>


<template>
  <main>

    <div class="flex justify-center items-center mt-8">
      <h1 class="text-3xl font-bold">
        Rick y Morty!!
      </h1>
    </div>

    <div class="flex justify-center mt-2">
      <button class="text-white bg-green-900 border-2 border-black rounded-sm p-2 mr-3" @click="incrementPage">+</button>
      {{ page }}
      <button class="bg-none text-white bg-red-900 border-2 border-black rounded-sm p-2 ml-3" @click="decrementPage">-</button>
    </div>

    <div class="grid grid-cols-2 sm:grid-cols-3 md:grid-cols-4 lg:grid-cols-5 xl:grid-cols-6 gap-7 mt-24 mx-10">
      <div v-for="character in characters" :key="character.id" class="rounded-2xl overflow-hidden shadow-2xl">
        <div @click="seeCharacterDetails(character.id)">
          <img class="rounded-t-3xl" :src="character.image" alt="character.name">
            <div class="m-4 text-center">
            {{ character.name }}
            </div>
        </div>
      </div>
    </div>

  </main>
</template>
