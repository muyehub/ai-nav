<template>
  <div 
    class="nav-card" 
    :class="size"
    :style="{ backgroundColor: bgColor }"
    @click="navigate"
  >
    <div class="content">
      <div class="icon" v-if="icon">
        <i :class="icon"></i>
      </div>
      <h3>{{ title }}</h3>
      <p v-if="description">{{ description }}</p>
    </div>
  </div>
</template>

<script setup lang="ts">
interface Props {
  title: string
  description?: string
  icon?: string
  size?: 'small' | 'medium' | 'large'
  bgColor?: string
  link?: string
}

const props = withDefaults(defineProps<Props>(), {
  size: 'medium',
  bgColor: '#2196F3',
})

const navigate = () => {
  if (props.link) {
    window.open(props.link, '_blank')
  }
}
</script>

<style scoped>
.nav-card {
  border-radius: 4px;
  padding: 20px;
  color: white;
  cursor: pointer;
  transition: transform 0.3s;
  overflow: hidden;
}

.nav-card:hover {
  transform: scale(1.05);
}

.small {
  grid-column: span 1;
  grid-row: span 1;
}

.medium {
  grid-column: span 2;
  grid-row: span 1;
}

.large {
  grid-column: span 2;
  grid-row: span 2;
}

.content {
  height: 100%;
  display: flex;
  flex-direction: column;
  justify-content: center;
}

.icon {
  font-size: 2em;
  margin-bottom: 10px;
}

h3 {
  margin: 0;
  font-size: 1.5em;
}

p {
  margin: 10px 0 0;
  opacity: 0.8;
}
</style> 