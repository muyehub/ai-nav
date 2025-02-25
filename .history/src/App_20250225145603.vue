<template>
  <div class="container">
    <div class="grid" v-for="(page, pageIndex) in Math.ceil(navItems.length / pageSize)" :key="pageIndex">
      <NavCard
        v-for="item in getPageItems(pageIndex)"
        :key="item.id"
        v-bind="item"
      />
    </div>
    <div class="load-more" v-if="displayedPages < Math.ceil(navItems.length / pageSize)" @click="loadMore">
      加载更多
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'
import NavCard from './components/NavCard.vue'

const pageSize = 12
const displayedPages = ref(1)

const navItems = ref([
  {
    id: 1,
    title: "通义灵码",
    description: "基于通义大模型的 AI 研发辅助工具",
    icon: "fas fa-code",
    bgColor: "#1890ff",
    link: "https://tongyi.aliyun.com/lingma"
  },
  {
    id: 2,
    title: "imageFX",
    description: "Google 实验室推出的文生图产品",
    icon: "fas fa-image",
    bgColor: "#FF4785",
    link: "https://imagefx.google"
  },
  {
    id: 3,
    title: "tldraw Computer",
    description: "无限画布的自然语言计算环境",
    icon: "fas fa-pencil-ruler",
    bgColor: "#2F80ED",
    link: "https://tldraw.com"
  },
  {
    id: 4,
    title: "ResearchFlow",
    description: "AI 驱动的研究引擎",
    icon: "fas fa-brain",
    bgColor: "#6B4FBB",
    link: "https://researchflow.ai"
  },
  {
    id: 5,
    title: "Eapy",
    description: "自由画布形式与 AI Music 结合",
    icon: "fas fa-music",
    bgColor: "#FF6B6B",
    link: "https://eapy.com"
  },
  {
    id: 6,
    title: "Midjourney Patchwork",
    description: "MidJourney 虚拟世界创建平台",
    icon: "fas fa-palette",
    bgColor: "#7B61FF",
    link: "https://www.midjourney.com"
  },
  {
    id: 7,
    title: "FunBlocks AIFlow",
    description: "AI 驱动的白板和思维导图工具",
    icon: "fas fa-project-diagram",
    bgColor: "#00B8D9",
    link: "https://funblocks.ai"
  },
  {
    id: 8,
    title: "Refly",
    description: "基于自由画布的创作平台",
    icon: "fas fa-pen-fancy",
    bgColor: "#36B37E",
    link: "https://refly.com"
  },
  {
    id: 9,
    title: "Claude",
    description: "Anthropic 开发的 AI 助手",
    icon: "fas fa-robot",
    bgColor: "#7C3AED",
    link: "https://claude.ai"
  },
  {
    id: 10,
    title: "ChatGPT",
    description: "OpenAI 的 AI 对话模型",
    icon: "fas fa-comments",
    bgColor: "#10A37F",
    link: "https://chat.openai.com"
  },
  {
    id: 11,
    title: "Gemini",
    description: "Google 最新的 AI 模型",
    icon: "fas fa-gem",
    bgColor: "#4285F4",
    link: "https://gemini.google.com"
  },
  {
    id: 12,
    title: "Copilot",
    description: "微软和 OpenAI 的 AI 助手",
    icon: "fas fa-terminal",
    bgColor: "#0D1117",
    link: "https://copilot.microsoft.com"
  },
  {
    id: 13,
    title: "文心一言",
    description: "百度的 AI 对话模型",
    icon: "fas fa-comment-dots",
    bgColor: "#2932E1",
    link: "https://yiyan.baidu.com"
  },
  {
    id: 14,
    title: "通义千问",
    description: "阿里的 AI 对话模型",
    icon: "fas fa-lightbulb",
    bgColor: "#FF6A00",
    link: "https://qianwen.aliyun.com"
  },
  {
    id: 15,
    title: "讯飞星火",
    description: "科大讯飞的认知大模型",
    icon: "fas fa-star",
    bgColor: "#FF4D4F",
    link: "https://xinghuo.xfyun.cn"
  },
  {
    id: 16,
    title: "Stable Diffusion",
    description: "开源图像生成模型",
    icon: "fas fa-paint-brush",
    bgColor: "#7B61FF",
    link: "https://stability.ai"
  },
  {
    id: 17,
    title: "Midjourney",
    description: "AI 图像生成服务",
    icon: "fas fa-image",
    bgColor: "#1A1A1A",
    link: "https://www.midjourney.com"
  },
  {
    id: 18,
    title: "DALL·E",
    description: "OpenAI 的图像生成模型",
    icon: "fas fa-palette",
    bgColor: "#FF4785",
    link: "https://openai.com/dall-e-3"
  },
  {
    id: 19,
    title: "文心一格",
    description: "百度的 AI 创作平台",
    icon: "fas fa-magic",
    bgColor: "#2932E1",
    link: "https://yige.baidu.com"
  },
  {
    id: 20,
    title: "Runway",
    description: "AI 视频生成和编辑",
    icon: "fas fa-film",
    bgColor: "#000000",
    link: "https://runway.ml"
  },
  {
    id: 21,
    title: "Synthesia",
    description: "AI 视频创作平台",
    icon: "fas fa-video",
    bgColor: "#6366F1",
    link: "https://www.synthesia.io"
  },
  {
    id: 22,
    title: "Descript",
    description: "AI 驱动的视频编辑器",
    icon: "fas fa-edit",
    bgColor: "#FF2D55",
    link: "https://www.descript.com"
  },
  {
    id: 23,
    title: "Murf",
    description: "AI 语音生成平台",
    icon: "fas fa-microphone",
    bgColor: "#7C3AED",
    link: "https://murf.ai"
  },
  {
    id: 24,
    title: "Notion AI",
    description: "集成 AI 的笔记工具",
    icon: "fas fa-book",
    bgColor: "#000000",
    link: "https://notion.so"
  },
  {
    id: 25,
    title: "Jasper",
    description: "AI 写作助手",
    icon: "fas fa-pen",
    bgColor: "#FF7A00",
    link: "https://www.jasper.ai"
  },
  {
    id: 26,
    title: "Copy.ai",
    description: "AI 文案生成工具",
    icon: "fas fa-copy",
    bgColor: "#2563EB",
    link: "https://www.copy.ai"
  },
  {
    id: 27,
    title: "Character.ai",
    description: "AI 角色对话平台",
    icon: "fas fa-user-circle",
    bgColor: "#FF6B6B",
    link: "https://character.ai"
  },
  {
    id: 28,
    title: "腾讯混元 3D",
    description: "腾讯推出的 3D 生成与处理 AI 工具平台",
    icon: "fas fa-cube",
    bgColor: "#2B5AED",
    link: "https://hunyuan.tencent.com/3d"
  },
  {
    id: 29,
    title: "百度自由画布",
    description: "百度文库和百度网盘联合推出的 AI 万能白板",
    icon: "fas fa-paint-brush",
    bgColor: "#3245E3",
    link: "https://ai.baidu.com/creation"
  },
  {
    id: 30,
    title: "Trae",
    description: "字节旗下的AI 编程 IDE",
    icon: "fas fa-laptop-code",
    bgColor: "#FF4D4F",
    link: "https://trae.ai"
  },
  {
    id: 31,
    title: "Day AI",
    description: "简化客户管理流程的 AI 工具",
    icon: "fas fa-calendar",
    bgColor: "#722ED1",
    link: "https://www.dayai.com"
  },
  {
    id: 32,
    title: "TOFU",
    description: "智能营销工具平台",
    icon: "fas fa-bullhorn",
    bgColor: "#FF6B6B",
    link: "https://tofu.ai"
  },
  {
    id: 33,
    title: "Nooks",
    description: "AI 智能销售助理",
    icon: "fas fa-handshake",
    bgColor: "#4CAF50",
    link: "https://nooks.ai"
  },
  {
    id: 34,
    title: "Quilt",
    description: "技术销售智能工具",
    icon: "fas fa-chart-line",
    bgColor: "#2196F3",
    link: "https://quilt.ai"
  },
  {
    id: 35,
    title: "Common Room",
    description: "智能市场推广平台",
    icon: "fas fa-users",
    bgColor: "#9C27B0",
    link: "https://commonroom.io"
  },
  {
    id: 36,
    title: "Unify",
    description: "AI 驱动的销售工具",
    icon: "fas fa-link",
    bgColor: "#3F51B5",
    link: "https://unify.ai"
  },
  {
    id: 37,
    title: "Genspark",
    description: "智能搜索引擎",
    icon: "fas fa-search",
    bgColor: "#FF9800",
    link: "https://genspark.ai"
  },
  {
    id: 38,
    title: "PictureThis",
    description: "AI 植物识别工具",
    icon: "fas fa-leaf",
    bgColor: "#4CAF50",
    link: "https://picturethisai.com"
  },
  {
    id: 39,
    title: "Zeemo",
    description: "AI 字幕生成工具",
    icon: "fas fa-closed-captioning",
    bgColor: "#607D8B",
    link: "https://zeemo.ai"
  },
  {
    id: 40,
    title: "Joyland",
    description: "AI 动漫角色互动平台",
    icon: "fas fa-smile-beam",
    bgColor: "#E91E63",
    link: "https://joyland.ai"
  },
  {
    id: 41,
    title: "YouCam",
    description: "AI 图像处理工具",
    icon: "fas fa-camera",
    bgColor: "#FF4081",
    link: "https://perfect-corp.com"
  },
  {
    id: 42,
    title: "Talkie",
    description: "AI 对话助手",
    icon: "fas fa-comments",
    bgColor: "#00BCD4",
    link: "https://talkie.ai"
  },
  {
    id: 43,
    title: "新华妙笔",
    description: "智能公文写作助手",
    icon: "fas fa-pen-fancy",
    bgColor: "#C62828",
    link: "https://xiaoice.com/miaobiapp"
  },
  {
    id: 44,
    title: "Alpha派",
    description: "AI 投研工具",
    icon: "fas fa-chart-bar",
    bgColor: "#1976D2",
    link: "https://alpha-pai.com"
  },
  {
    id: 45,
    title: "Reecho睿声",
    description: "AI 音效生成平台",
    icon: "fas fa-music",
    bgColor: "#673AB7",
    link: "https://reecho.ai"
  },
  {
    id: 46,
    title: "百度 AI 探索版",
    description: "百度 AI 实验室",
    icon: "fas fa-flask",
    bgColor: "#2932E1",
    link: "https://ai.baidu.com/explorer"
  },
  {
    id: 47,
    title: "PTE猩际",
    description: "AI 驱动的考试平台",
    icon: "fas fa-graduation-cap",
    bgColor: "#F44336",
    link: "https://pteplus.com.au"
  },
  {
    id: 48,
    title: "纳米 AI 搜索",
    description: "智能搜索引擎",
    icon: "fas fa-search-plus",
    bgColor: "#009688",
    link: "https://nami.ai"
  },
  {
    id: 49,
    title: "钉钉宜搭",
    description: "阿里低代码平台",
    icon: "fas fa-tools",
    bgColor: "#1890FF",
    link: "https://yida.alibaba-inc.com"
  },
  {
    id: 50,
    title: "知乎直答",
    description: "AI 问答助手",
    icon: "fas fa-question-circle",
    bgColor: "#0084FF",
    link: "https://zhihu.com/ai"
  },
  {
    id: 51,
    title: "C知道",
    description: "CSDN AI 助手",
    icon: "fas fa-code",
    bgColor: "#FC5531",
    link: "https://csdn.net/ai"
  }
])

const getPageItems = (pageIndex: number) => {
  const start = pageIndex * pageSize
  const end = start + pageSize
  return navItems.value.slice(start, end)
}

const loadMore = () => {
  displayedPages.value++
}
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

.load-more {
  text-align: center;
  padding: 20px;
  margin-top: 20px;
  background-color: #fff;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
}

.load-more:hover {
  background-color: #f5f5f5;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}
</style>

    padding: 10px;