<template>
  <div class="app">
    <MetroNav />
  </div>
</template>

<script setup lang="ts">
import { defineComponent } from 'vue'
import MetroNav from '../../src/components/MetroNav.vue'
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  font-family: Arial, sans-serif;
}
</style> 