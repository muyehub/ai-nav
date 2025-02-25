<template>
  <a :href="link" class="nav-card" :class="size" :style="{ backgroundColor: bgColor }" target="_blank">
    <i :class="icon"></i>
    <h3>{{ title }}</h3>
    <p v-if="description">{{ description }}</p>
  </a>
</template>

<script setup lang="ts">
defineOptions({
  name: 'NavCard'
})

defineProps<{
  title: string
  description?: string
  icon: string
  bgColor: string
  link: string
  size?: 'small' | 'medium' | 'large'
}>()
</script>

<style scoped>
.nav-card {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 20px;
  color: white;
  text-decoration: none;
  border-radius: 10px;
  transition: transform 0.3s;
  aspect-ratio: 1;
}

.nav-card:hover {
  transform: translateY(-5px);
}

.large { grid-column: span 2; grid-row: span 2; }
.medium { grid-column: span 2; }

i { font-size: 2em; margin-bottom: 10px; }
h3 { margin: 10px 0; }
p { margin: 0; font-size: 0.9em; opacity: 0.9; }
</style>