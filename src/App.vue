<script setup>
  import { ref,computed } from "vue";
  const counter = ref(0);
  const favorites = ref([])

  const dinamicColor = computed(() => {
    if(counter.value === 0) 
      return "text-blue-600"
    else if(counter.value < 0) 
      return 'text-red-600'
    else if(counter.value > 0)
      return 'text-green-600'
  })

  const blockBtn = computed(()=> (favorites.value.includes(counter.value) ? true : false))

  const increase = () => {
    counter.value++;
  }
  const decrease = () => {
    counter.value--;
  }
  const reset = () => {
    counter.value = 0;
  }
  const addToFavorites = () => {
    if(favorites.value.includes(counter.value)) return
    favorites.value.push(counter.value)
  }
</script>

<template>
  <div class="grid w-screen h-screen place-content-center space-y-4">
    <h1 class="text-6xl text-center" :class="dinamicColor">{{ counter }}</h1>
    <button @click="increase" class="bg-green-300 text-green-950 px-3 py-1 transition-all hover:scale-105">Aumentar</button>
    <button @click="decrease" class="bg-red-300 text-red-950 px-3 py-1 transition-all hover:scale-105">Disminuir</button>
    <button @click="reset" class="bg-blue-300 text-blue-950 px-3 py-1 transition-all hover:scale-105">Resetear</button>
    <button @click="addToFavorites" class="bg-orange-300 text-orange-950 px-3 py-1 transition-all hover:scale-105 disabled:bg-gray-400 disabled:text-gray-600" :disabled="blockBtn">Agregar a favoritos</button>
    <span v-show="favorites.length == 0">No hay numeros en la lista</span>
    <template v-if="favorites.length > 0">
      <ul v-for="number in favorites" :key="number">
        <li>{{ number }}</li>
      </ul>
    </template>
  </div>

</template>
