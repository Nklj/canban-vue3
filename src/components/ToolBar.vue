<template>
  <div class="card" :style="`background: ${options.color}`">
    <v-tooltip text="Сортировка по убыванию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort-descending"
          density="compact"
          variant="tonal"
          class="mr-2"
          color="grey"
          @click="descSortList" />
      </template>
    </v-tooltip>
    <v-tooltip text="Сортировка по возрастанию рейтинга">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort-ascending"
          density="compact"
          variant="tonal"
          class="mr-2"
          color="grey"
          @click="ascSortList" />
      </template>
    </v-tooltip>
    <v-tooltip text="Сброс сортировки">
      <template v-slot:activator="{ props }">
        <v-btn
          v-bind="props"
          icon="mdi-sort-variant-remove"
          density="compact"
          variant="tonal"
          class=""
          color="grey"
          @click="cancelSortList" />
      </template>
    </v-tooltip>
  </div>
</template>

<script script setup>
  import { ref, inject, computed } from 'vue';

  const firstList = inject('firstList');
  const secondList = inject('secondList');
  const lastList = inject('lastList');

  const props = defineProps({
    options: {},
  });

  let cards = ref([])
  const initialCards = ref([])

  function getLocalCards() {
    switch (props.options.id) {
      case 1:
        cards = firstList;        
        break;
      case 2:
        cards = secondList;
        break;
      case 3:
        cards = lastList;
        break;
    }
    if(initialCards.value.length===0) initialCards.value = [...cards.value];
  }

  function descSortList() {
    getLocalCards();
    cards = cards.value.sort((a, b) => b.rating.rate - a.rating.rate);
  }
  function ascSortList() {
    getLocalCards();
    cards = cards.value.sort((a, b) => a.rating.rate - b.rating.rate);
  }
  function cancelSortList() {
    getLocalCards(); 
    cards = cards.value.sort((a, b) => a.id - b.id);   
  }
  
</script>  

<style lang="scss" scoped>
  .card {    
    padding: 3%;
    width: 100%;
    display: flex;
    justify-content: end;
    align-items: center;
    background-color: rgb(255, 255, 255);
    border-radius: 10px;  
    position: absolute; 
    top: -8vh;    
  }
</style>
