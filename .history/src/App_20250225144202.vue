<template>
  <div class="container">
    <div class="grid">
      <NavCard
        title="GitHub"
        description="代码托管平台"
        icon="fab fa-github"
        bgColor="#24292e"
        link="https://github.com"
        size="large"
      />
      <NavCard
        title="Google"
        icon="fab fa-google"
        bgColor="#4285F4"
        link="https://google.com"
      />
      <NavCard
        title="Twitter"
        icon="fab fa-twitter"
        bgColor="#1DA1F2"
        link="https://twitter.com"
      />
      <NavCard
        title="YouTube"
        description="视频分享平台"
        icon="fab fa-youtube"
        bgColor="#FF0000"
        size="medium"
        link="https://youtube.com"
      />
      <!-- 可以继续添加更多导航卡片 -->
    </div>
  </div>
</template>

<script setup lang="ts">
import NavCard from './components/NavCard.vue'
</script>

<style>
body {
  margin: 0;
  padding: 0;
  background-color: #f0f0f0;
  min-height: 100vh;
}

.container {
  padding: 20px;
  box-sizing: border-box;
  min-height: 100vh;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  gap: 20px;
  max-width: 1200px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .grid {
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
  }
}
</style> 