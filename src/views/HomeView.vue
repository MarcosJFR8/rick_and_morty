<script setup lang="ts">
import { onMounted, ref, } from 'vue'
import { useRouter } from 'vue-router'
import type { Character } from '@/types/character'


const page = ref<number>(1)
const router = useRouter()
const characters = ref<Character[]>([])
const searchName = ref<string>('')
const searchStatus = ref<string>('')
const nextPage = ref<number>()
const statusFilters = ['', 'Alive', 'Dead', 'unknown']



const searchByStatus = (status: string)=>{
  page.value = 1
  searchStatus.value = status
  loadCharacters()
}

const findCharacters = () => {
  loadCharacters()
}

const loadCharacters = async () => {
  const response = await fetch(`https://rickandmortyapi.com/api/character?page=${page.value}&name=${searchName.value}&status=${searchStatus.value}`)
  const data = await response.json()
  nextPage.value =data.info.next
  characters.value = data.results
}

const incrementPage = () => {
  if (nextPage.value !== null){
    page.value++
    loadCharacters()
  }
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


  <div class="flex flex-col items-center mt-8">
      <input @change="findCharacters" class="border-blue-900 border-2 justify object-top " v-model="searchName" type="text">
      <div class="flex space-x-4 mt-4">
        <button v-for="status in statusFilters" :class= "['bg-black text-white p2 rounded-full', 
          searchStatus === status ? 'bg-red-500' : 'bg-black']" 
          @click="searchByStatus(status)"> 
          {{ status === '' ? 'All' : status }} 
        </button>
      </div>
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
