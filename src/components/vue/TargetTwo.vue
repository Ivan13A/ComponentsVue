<script setup>
import { ref, onMounted } from 'vue';

const tarjetas = ref([]);

const fetchQuotes = async () => {
  try {
    const response = await fetch('https://thesimpsonsquoteapi.glitch.me/quotes?count=10');
    const data = await response.json();
    tarjetas.value = data;
  } catch (error) {
    console.error('Error al obtener los datos:', error);
  }
};

onMounted(fetchQuotes);
</script>

<template>
  <section class="max-w-7xl mx-auto py-10">
    <div v-for="(tarjeta, index) in tarjetas" :key="index" class="w-[500px] mx-auto my-6 bg-yellow-600 p-3 rounded-lg">
      <div :class="['p-6 bg-slate-200 rounded-lg flex items-center', tarjeta.characterDirection === 'Right' ? 'flex-row-reverse' : 'flex-row']">
        <div class="w-[125px] m-4">
          <img class="rounded-full" :src="tarjeta.image" :alt="`Imagen de ${tarjeta.character}`">
        </div>
        <div class="font-semibold">
          <div class="uppercase text-xl mb-2">{{ tarjeta.character }}</div>
          <div class="mb-2 flex">
            <p class="ml-1 font-normal">{{ tarjeta.quote }}</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>