<template>
  <div class="container">
    <div class="grid">
      <NavCard
        title="通义灵码"
        description="基于通义大模型的 AI 研发辅助工具"
        icon="fas fa-code"
        bgColor="#1890ff"
        link="https://tongyi.aliyun.com/lingma"
        size="medium"
      />
      <NavCard
        title="imageFX"
        description="Google 实验室推出的文生图产品"
        icon="fas fa-image"
        bgColor="#FF4785"
        link="https://imagefx.google"
        size="medium"
      />
      <NavCard
        title="tldraw Computer"
        description="无限画布的自然语言计算环境"
        icon="fas fa-pencil-ruler"
        bgColor="#2F80ED"
        link="https://tldraw.com"
        size="large"
      />
      <NavCard
        title="ResearchFlow"
        description="AI 驱动的研究引擎"
        icon="fas fa-brain"
        bgColor="#6B4FBB"
        link="https://researchflow.ai"
      />
      <NavCard
        title="Eapy"
        description="自由画布形式与 AI Music 结合"
        icon="fas fa-music"
        bgColor="#FF6B6B"
        link="https://eapy.com"
      />
      <NavCard
        title="Midjourney Patchwork"
        description="MidJourney 虚拟世界创建平台"
        icon="fas fa-palette"
        bgColor="#7B61FF"
        link="https://www.midjourney.com"
        size="large"
      />
      <NavCard
        title="FunBlocks AIFlow"
        description="AI 驱动的白板和思维导图工具"
        icon="fas fa-project-diagram"
        bgColor="#00B8D9"
        link="https://funblocks.ai"
      />
      <NavCard
        title="Refly"
        description="基于自由画布的创作平台"
        icon="fas fa-pen-fancy"
        bgColor="#36B37E"
        link="https://refly.com"
      />
      <!-- 继续添加更多导航卡片... -->
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
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.container {
  padding: 20px;
  box-sizing: border-box;
  min-height: 100vh;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  max-width: 1400px;
  margin: 0 auto;
}

@media (max-width: 768px) {
  .grid {
    grid-template-columns: repeat(auto-fill, minmax(150px, 1fr));
  }
}
</style>
