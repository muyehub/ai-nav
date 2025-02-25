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
      <NavCard
        title="Claude"
        description="Anthropic 开发的 AI 助手"
        icon="fas fa-robot"
        bgColor="#7C3AED"
        link="https://claude.ai"
        size="medium"
      />
      <NavCard
        title="ChatGPT"
        description="OpenAI 的 AI 对话模型"
        icon="fas fa-comments"
        bgColor="#10A37F"
        link="https://chat.openai.com"
        size="medium"
      />
      <NavCard
        title="Gemini"
        description="Google 最新的 AI 模型"
        icon="fas fa-gem"
        bgColor="#4285F4"
        link="https://gemini.google.com"
      />
      <NavCard
        title="Copilot"
        description="微软和 OpenAI 的 AI 助手"
        icon="fas fa-terminal"
        bgColor="#0D1117"
        link="https://copilot.microsoft.com"
      />
      <NavCard
        title="文心一言"
        description="百度的 AI 对话模型"
        icon="fas fa-comment-dots"
        bgColor="#2932E1"
        link="https://yiyan.baidu.com"
      />
      <NavCard
        title="通义千问"
        description="阿里的 AI 对话模型"
        icon="fas fa-lightbulb"
        bgColor="#FF6A00"
        link="https://qianwen.aliyun.com"
      />
      <NavCard
        title="讯飞星火"
        description="科大讯飞的认知大模型"
        icon="fas fa-star"
        bgColor="#FF4D4F"
        link="https://xinghuo.xfyun.cn"
      />
      <NavCard
        title="Stable Diffusion"
        description="开源图像生成模型"
        icon="fas fa-paint-brush"
        bgColor="#7B61FF"
        link="https://stability.ai"
        size="large"
      />
      <NavCard
        title="Midjourney"
        description="AI 图像生成服务"
        icon="fas fa-image"
        bgColor="#1A1A1A"
        link="https://www.midjourney.com"
        size="medium"
      />
      <NavCard
        title="DALL·E"
        description="OpenAI 的图像生成模型"
        icon="fas fa-palette"
        bgColor="#FF4785"
        link="https://openai.com/dall-e-3"
      />
      <NavCard
        title="文心一格"
        description="百度的 AI 创作平台"
        icon="fas fa-magic"
        bgColor="#2932E1"
        link="https://yige.baidu.com"
      />
      <NavCard
        title="Runway"
        description="AI 视频生成和编辑"
        icon="fas fa-film"
        bgColor="#000000"
        link="https://runway.ml"
        size="large"
      />
      <NavCard
        title="Synthesia"
        description="AI 视频创作平台"
        icon="fas fa-video"
        bgColor="#6366F1"
        link="https://www.synthesia.io"
      />
      <NavCard
        title="Descript"
        description="AI 驱动的视频编辑器"
        icon="fas fa-edit"
        bgColor="#FF2D55"
        link="https://www.descript.com"
      />
      <NavCard
        title="Murf"
        description="AI 语音生成平台"
        icon="fas fa-microphone"
        bgColor="#7C3AED"
        link="https://murf.ai"
      />
      <NavCard
        title="Notion AI"
        description="集成 AI 的笔记工具"
        icon="fas fa-book"
        bgColor="#000000"
        link="https://notion.so"
        size="medium"
      />
      <NavCard
        title="Jasper"
        description="AI 写作助手"
        icon="fas fa-pen"
        bgColor="#FF7A00"
        link="https://www.jasper.ai"
      />
      <NavCard
        title="Copy.ai"
        description="AI 文案生成工具"
        icon="fas fa-copy"
        bgColor="#2563EB"
        link="https://www.copy.ai"
      />
      <NavCard
        title="Character.ai"
        description="AI 角色对话平台"
        icon="fas fa-user-circle"
        bgColor="#FF6B6B"
        link="https://character.ai"
        size="medium"
      />
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
  width: 100%;
}

.grid {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 20px;
  width: 100%;
  max-width: 1800px;
  margin: 0 auto;
}

/* 平板设备 */
@media (max-width: 1024px) {
  .grid {
    grid-template-columns: repeat(auto-fill, minmax(160px, 1fr));
    gap: 15px;
  }
  
  .container {
    padding: 15px;
  }
}

/* 手机设备 */
@media (max-width: 768px) {
  .grid {
    grid-template-columns: repeat(auto-fill, minmax(120px, 1fr));
    gap: 10px;
  }
  
  .container {
    padding: 10px;
  }
}
</style>

    padding: 10px;