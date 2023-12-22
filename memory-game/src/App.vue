<template>
  <Card :character-name="'Gael'"  :url-image="'src/assets/images/gael2.jpg'"></Card>
  <img src="./assets/images/" alt="">
  <RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import { ref } from 'vue';
import Card from './components/Card.vue';


</script>


<style scoped>

</style>
