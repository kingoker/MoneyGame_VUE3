<script setup>
  import { RouterView } from 'vue-router';
  import Header from './components/Header.vue'
  import DiceOrDice from './components/DiceOrDice.vue';
  import MetaphoricalCards from './components/MetaphoricalCards.vue'
</script>

<template>
  <!-- Шапка -->
  <!-- <Header></Header> -->


  <!-- Основная часть сайта -->
  <RouterView />


  <!-- Метофорические карты -->
  <MetaphoricalCards></MetaphoricalCards>

  <!-- Игровые кубики -->
  <DiceOrDice></DiceOrDice>


  <!-- Подвал сайта -->

</template>

<style scoped>
  .margin_top_50{
    margin-top: 50px;
  }
</style>
