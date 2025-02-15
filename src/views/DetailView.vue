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


<template>
    <div v-if="character">
        {{ character.name }}
    </div>
</template>