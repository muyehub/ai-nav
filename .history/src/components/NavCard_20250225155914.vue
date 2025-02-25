<template>
  <a :href="link" class="nav-card" :class="size" :style="{ backgroundColor: bgColor }" target="_blank">
    <i :class="icon"></i>
    <h3>{{ title }}</h3>
    <p v-if="description">{{ description }}</p>
  </a>
</template>

<script setup lang="ts">
defineOptions({
  name: 'NavCard',
  inheritAttrs: false
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
  padding: 15px;
  color: white;
  text-decoration: none;
  border-radius: 8px;
  transition: transform 0.3s;
  aspect-ratio: 1;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.nav-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.2);
}

.large { 
  grid-column: span 1;
  grid-row: span 1;
  font-size: 1.1em;
}

.medium { 
  grid-column: span 1;
  font-size: 1em;
}

i { font-size: 1.8em; margin-bottom: 8px; }
h3 { margin: 8px 0; font-size: 1em; }
p { 
  margin: 0; 
  font-size: 0.8em; 
  opacity: 0.9; 
  text-align: center;
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
}
</style>