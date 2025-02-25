<template>
  <div class="metro-container">
    <div class="metro-grid">
      <a 
        v-for="item in navItems" 
        :key="item.id"
        :href="item.url"
        class="metro-item"
        :class="item.size"
        :style="{ backgroundColor: item.color }"
        target="_blank"
      >
        <span class="title">{{ item.title }}</span>
      </a>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import type { NavItem } from '../types'

// 添加默认导出
defineOptions({
  name: 'MetroNav'
})

const navItems = ref<NavItem[]>([
  {
    id: 1,
    title: '谷歌',
    url: 'https://google.com',
    color: '#4285f4',
    size: 'large'
  },
  {
    id: 2,
    title: '哔哩哔哩',
    url: 'https://bilibili.com',
    color: '#fb7299',
    size: 'medium'
  },
  {
    id: 3,
    title: '知乎',
    url: 'https://zhihu.com',
    color: '#0084ff',
    size: 'small'
  },
  // 可以继续添加更多导航项
])
</script>

<style scoped>
.metro-container {
  min-height: 100vh;
  padding: 2rem;
  background: #f0f0f0;
}

.metro-grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 1rem;
  max-width: 1200px;
  margin: 0 auto;
}

.metro-item {
  position: relative;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  text-decoration: none;
  border-radius: 8px;
  transition: all 0.3s ease;
  aspect-ratio: 1;
}

.metro-item:hover {
  transform: translateY(-5px);
  box-shadow: 0 5px 15px rgba(0, 0, 0, 0.3);
}

.metro-item.small {
  grid-column: span 1;
  grid-row: span 1;
}

.metro-item.medium {
  grid-column: span 2;
  grid-row: span 1;
}

.metro-item.large {
  grid-column: span 2;
  grid-row: span 2;
}

.title {
  font-size: 1.2rem;
  font-weight: bold;
  text-align: center;
}
</style> 