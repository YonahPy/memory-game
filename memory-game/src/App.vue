<template>
  <div>ola mundo</div>
  <card></card>
  <RouterView />
</template>

<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import card from './components/card.vue';
</script>

<style scoped>

</style>
