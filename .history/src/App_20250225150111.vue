<template>
  <div class="container">
    <div class="header">
      <h1>硅基涌动</h1>
      <p>探索 AI 工具的无限可能</p>
    </div>
    <div class="category-filter">
      <button 
        v-for="category in categories" 
        :key="category.value"
        :class="['category-btn', { active: currentCategory === category.value }]"
        @click="setCategory(category.value)"
      >
        {{ category.label }}
      </button>
    </div>
    <div class="grid">
      <NavCard
        v-for="item in filteredItems"
        :key="item.id"
        v-bind="item"
      />
    </div>
    <div class="load-more" v-if="hasMoreItems" @click="loadMore" ref="loadMoreRef">
      <template v-if="!loading">加载更多</template>
      <div v-else class="loading-spinner"></div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, onMounted, onUnmounted } from 'vue'
import NavCard from './components/NavCard.vue'

const pageSize = 12
const currentPage = ref(1)
const loading = ref(false)
const loadMoreRef = ref<HTMLElement | null>(null)

// 定义分类
const categories = [
  { label: '全部', value: 'all' },
  { label: '对话模型', value: 'chat' },
  { label: '图像生成', value: 'image' },
  { label: '视频创作', value: 'video' },
  { label: '音频处理', value: 'audio' },
  { label: '开发工具', value: 'dev' },
  { label: '办公效率', value: 'office' },
  { label: '营销工具', value: 'marketing' },
]

const currentCategory = ref('all')

const navItems = ref([
  {
    id: 1,
    title: "通义灵码",
    description: "基于通义大模型的 AI 研发辅助工具",
    icon: "fas fa-code",
    bgColor: "#1890ff",
    link: "https://tongyi.aliyun.com/lingma",
    category: "dev"
  },
  {
    id: 2,
    title: "imageFX",
    description: "Google 实验室推出的文生图产品",
    icon: "fas fa-image",
    bgColor: "#FF4785",
    link: "https://imagefx.google",
    category: "image"
  },
  {
    id: 3,
    title: "tldraw Computer",
    description: "无限画布的自然语言计算环境",
    icon: "fas fa-pencil-ruler",
    bgColor: "#2F80ED",
    link: "https://tldraw.com",
    category: "dev"
  },
  {
    id: 4,
    title: "ResearchFlow",
    description: "AI 驱动的研究引擎",
    icon: "fas fa-brain",
    bgColor: "#6B4FBB",
    link: "https://researchflow.ai",
    category: "dev"
  },
  {
    id: 5,
    title: "Eapy",
    description: "自由画布形式与 AI Music 结合",
    icon: "fas fa-music",
    bgColor: "#FF6B6B",
    link: "https://eapy.com",
    category: "audio"
  },
  {
    id: 6,
    title: "Midjourney Patchwork",
    description: "MidJourney 虚拟世界创建平台",
    icon: "fas fa-palette",
    bgColor: "#7B61FF",
    link: "https://www.midjourney.com",
    category: "image"
  },
  {
    id: 7,
    title: "FunBlocks AIFlow",
    description: "AI 驱动的白板和思维导图工具",
    icon: "fas fa-project-diagram",
    bgColor: "#00B8D9",
    link: "https://funblocks.ai",
    category: "dev"
  },
  {
    id: 8,
    title: "Refly",
    description: "基于自由画布的创作平台",
    icon: "fas fa-pen-fancy",
    bgColor: "#36B37E",
    link: "https://refly.com",
    category: "dev"
  },
  {
    id: 9,
    title: "Claude",
    description: "Anthropic 开发的 AI 助手",
    icon: "fas fa-robot",
    bgColor: "#7C3AED",
    link: "https://claude.ai",
    category: "chat"
  },
  {
    id: 10,
    title: "ChatGPT",
    description: "OpenAI 的 AI 对话模型",
    icon: "fas fa-comments",
    bgColor: "#10A37F",
    link: "https://chat.openai.com",
    category: "chat"
  },
  {
    id: 11,
    title: "Gemini",
    description: "Google 最新的 AI 模型",
    icon: "fas fa-gem",
    bgColor: "#4285F4",
    link: "https://gemini.google.com",
    category: "dev"
  },
  {
    id: 12,
    title: "Copilot",
    description: "微软和 OpenAI 的 AI 助手",
    icon: "fas fa-terminal",
    bgColor: "#0D1117",
    link: "https://copilot.microsoft.com",
    category: "dev"
  },
  {
    id: 13,
    title: "文心一言",
    description: "百度的 AI 对话模型",
    icon: "fas fa-comment-dots",
    bgColor: "#2932E1",
    link: "https://yiyan.baidu.com",
    category: "chat"
  },
  {
    id: 14,
    title: "通义千问",
    description: "阿里的 AI 对话模型",
    icon: "fas fa-lightbulb",
    bgColor: "#FF6A00",
    link: "https://qianwen.aliyun.com",
    category: "chat"
  },
  {
    id: 15,
    title: "讯飞星火",
    description: "科大讯飞的认知大模型",
    icon: "fas fa-star",
    bgColor: "#FF4D4F",
    link: "https://xinghuo.xfyun.cn",
    category: "dev"
  },
  {
    id: 16,
    title: "Stable Diffusion",
    description: "开源图像生成模型",
    icon: "fas fa-paint-brush",
    bgColor: "#7B61FF",
    link: "https://stability.ai",
    category: "image"
  },
  {
    id: 17,
    title: "Midjourney",
    description: "AI 图像生成服务",
    icon: "fas fa-image",
    bgColor: "#1A1A1A",
    link: "https://www.midjourney.com",
    category: "image"
  },
  {
    id: 18,
    title: "DALL·E",
    description: "OpenAI 的图像生成模型",
    icon: "fas fa-palette",
    bgColor: "#FF4785",
    link: "https://openai.com/dall-e-3",
    category: "image"
  },
  {
    id: 19,
    title: "文心一格",
    description: "百度的 AI 创作平台",
    icon: "fas fa-magic",
    bgColor: "#2932E1",
    link: "https://yige.baidu.com",
    category: "dev"
  },
  {
    id: 20,
    title: "Runway",
    description: "AI 视频生成和编辑",
    icon: "fas fa-film",
    bgColor: "#000000",
    link: "https://runway.ml",
    category: "video"
  },
  {
    id: 21,
    title: "Synthesia",
    description: "AI 视频创作平台",
    icon: "fas fa-video",
    bgColor: "#6366F1",
    link: "https://www.synthesia.io",
    category: "video"
  },
  {
    id: 22,
    title: "Descript",
    description: "AI 驱动的视频编辑器",
    icon: "fas fa-edit",
    bgColor: "#FF2D55",
    link: "https://www.descript.com",
    category: "video"
  },
  {
    id: 23,
    title: "Murf",
    description: "AI 语音生成平台",
    icon: "fas fa-microphone",
    bgColor: "#7C3AED",
    link: "https://murf.ai",
    category: "audio"
  },
  {
    id: 24,
    title: "Notion AI",
    description: "集成 AI 的笔记工具",
    icon: "fas fa-book",
    bgColor: "#000000",
    link: "https://notion.so",
    category: "office"
  },
  {
    id: 25,
    title: "Jasper",
    description: "AI 写作助手",
    icon: "fas fa-pen",
    bgColor: "#FF7A00",
    link: "https://www.jasper.ai",
    category: "office"
  },
  {
    id: 26,
    title: "Copy.ai",
    description: "AI 文案生成工具",
    icon: "fas fa-copy",
    bgColor: "#2563EB",
    link: "https://www.copy.ai",
    category: "office"
  },
  {
    id: 27,
    title: "Character.ai",
    description: "AI 角色对话平台",
    icon: "fas fa-user-circle",
    bgColor: "#FF6B6B",
    link: "https://character.ai",
    category: "chat"
  },
  {
    id: 28,
    title: "腾讯混元 3D",
    description: "腾讯推出的 3D 生成与处理 AI 工具平台",
    icon: "fas fa-cube",
    bgColor: "#2B5AED",
    link: "https://hunyuan.tencent.com/3d",
    category: "dev"
  },
  {
    id: 29,
    title: "百度自由画布",
    description: "百度文库和百度网盘联合推出的 AI 万能白板",
    icon: "fas fa-paint-brush",
    bgColor: "#3245E3",
    link: "https://ai.baidu.com/creation",
    category: "dev"
  },
  {
    id: 30,
    title: "Trae",
    description: "字节旗下的AI 编程 IDE",
    icon: "fas fa-laptop-code",
    bgColor: "#FF4D4F",
    link: "https://trae.ai",
    category: "dev"
  },
  {
    id: 31,
    title: "Day AI",
    description: "简化客户管理流程的 AI 工具",
    icon: "fas fa-calendar",
    bgColor: "#722ED1",
    link: "https://www.dayai.com",
    category: "office"
  },
  {
    id: 32,
    title: "TOFU",
    description: "智能营销工具平台",
    icon: "fas fa-bullhorn",
    bgColor: "#FF6B6B",
    link: "https://tofu.ai",
    category: "marketing"
  },
  {
    id: 33,
    title: "Nooks",
    description: "AI 智能销售助理",
    icon: "fas fa-handshake",
    bgColor: "#4CAF50",
    link: "https://nooks.ai",
    category: "office"
  },
  {
    id: 34,
    title: "Quilt",
    description: "技术销售智能工具",
    icon: "fas fa-chart-line",
    bgColor: "#2196F3",
    link: "https://quilt.ai",
    category: "marketing"
  },
  {
    id: 35,
    title: "Common Room",
    description: "智能市场推广平台",
    icon: "fas fa-users",
    bgColor: "#9C27B0",
    link: "https://commonroom.io",
    category: "marketing"
  },
  {
    id: 36,
    title: "Unify",
    description: "AI 驱动的销售工具",
    icon: "fas fa-link",
    bgColor: "#3F51B5",
    link: "https://unify.ai",
    category: "marketing"
  },
  {
    id: 37,
    title: "Genspark",
    description: "智能搜索引擎",
    icon: "fas fa-search",
    bgColor: "#FF9800",
    link: "https://genspark.ai",
    category: "dev"
  },
  {
    id: 38,
    title: "PictureThis",
    description: "AI 植物识别工具",
    icon: "fas fa-leaf",
    bgColor: "#4CAF50",
    link: "https://picturethisai.com",
    category: "image"
  },
  {
    id: 39,
    title: "Zeemo",
    description: "AI 字幕生成工具",
    icon: "fas fa-closed-captioning",
    bgColor: "#607D8B",
    link: "https://zeemo.ai",
    category: "office"
  },
  {
    id: 40,
    title: "Joyland",
    description: "AI 动漫角色互动平台",
    icon: "fas fa-smile-beam",
    bgColor: "#E91E63",
    link: "https://joyland.ai",
    category: "chat"
  },
  {
    id: 41,
    title: "YouCam",
    description: "AI 图像处理工具",
    icon: "fas fa-camera",
    bgColor: "#FF4081",
    link: "https://perfect-corp.com",
    category: "image"
  },
  {
    id: 42,
    title: "Talkie",
    description: "AI 对话助手",
    icon: "fas fa-comments",
    bgColor: "#00BCD4",
    link: "https://talkie.ai",
    category: "chat"
  },
  {
    id: 43,
    title: "新华妙笔",
    description: "智能公文写作助手",
    icon: "fas fa-pen-fancy",
    bgColor: "#C62828",
    link: "https://xiaoice.com/miaobiapp",
    category: "office"
  },
  {
    id: 44,
    title: "Alpha派",
    description: "AI 投研工具",
    icon: "fas fa-chart-bar",
    bgColor: "#1976D2",
    link: "https://alpha-pai.com",
    category: "dev"
  },
  {
    id: 45,
    title: "Reecho睿声",
    description: "AI 音效生成平台",
    icon: "fas fa-music",
    bgColor: "#673AB7",
    link: "https://reecho.ai",
    category: "audio"
  },
  {
    id: 46,
    title: "百度 AI 探索版",
    description: "百度 AI 实验室",
    icon: "fas fa-flask",
    bgColor: "#2932E1",
    link: "https://ai.baidu.com/explorer",
    category: "dev"
  },
  {
    id: 47,
    title: "PTE猩际",
    description: "AI 驱动的考试平台",
    icon: "fas fa-graduation-cap",
    bgColor: "#F44336",
    link: "https://pteplus.com.au",
    category: "office"
  },
  {
    id: 48,
    title: "纳米 AI 搜索",
    description: "智能搜索引擎",
    icon: "fas fa-search-plus",
    bgColor: "#009688",
    link: "https://nami.ai",
    category: "dev"
  },
  {
    id: 49,
    title: "钉钉宜搭",
    description: "阿里低代码平台",
    icon: "fas fa-tools",
    bgColor: "#1890FF",
    link: "https://yida.alibaba-inc.com",
    category: "dev"
  },
  {
    id: 50,
    title: "知乎直答",
    description: "AI 问答助手",
    icon: "fas fa-question-circle",
    bgColor: "#0084FF",
    link: "https://zhihu.com/ai",
    category: "chat"
  },
  {
    id: 51,
    title: "C知道",
    description: "CSDN AI 助手",
    icon: "fas fa-code",
    bgColor: "#FC5531",
    link: "https://csdn.net/ai",
    category: "dev"
  }
])

const filteredItems = computed(() => {
  const items = currentCategory.value === 'all' 
    ? navItems.value 
    : navItems.value.filter(item => item.category === currentCategory.value)
  return items.slice(0, currentPage.value * pageSize)
})

const hasMoreItems = computed(() => {
  const totalItems = currentCategory.value === 'all'
    ? navItems.value.length
    : navItems.value.filter(item => item.category === currentCategory.value).length
  return filteredItems.value.length < totalItems
})

const loadMore = async () => {
  if (loading.value) return
  
  loading.value = true
  // 模拟加载延迟
  await new Promise(resolve => setTimeout(resolve, 500))
  currentPage.value++
  loading.value = false
}

// 实现滚动加载
const observer = ref<IntersectionObserver | null>(null)

onMounted(() => {
  observer.value = new IntersectionObserver(([entry]) => {
    if (entry.isIntersecting && hasMoreItems.value && !loading.value) {
      loadMore()
    }
  })

  if (loadMoreRef.value) {
    observer.value.observe(loadMoreRef.value)
  }
})

onUnmounted(() => {
  if (observer.value) {
    observer.value.disconnect()
  }
})

const setCategory = (category: string) => {
  currentCategory.value = category
  currentPage.value = 1 // 重置页码
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
  animation: fadeIn 0.3s ease-in-out;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
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
  margin: 20px auto;
  background-color: #fff;
  border-radius: 8px;
  cursor: pointer;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
  transition: all 0.3s;
  max-width: 200px;
}

.load-more:hover {
  background-color: #f5f5f5;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
}

.loading-spinner {
  width: 30px;
  height: 30px;
  margin: 0 auto;
  border: 3px solid #f3f3f3;
  border-top: 3px solid #3498db;
  border-radius: 50%;
  animation: spin 1s linear infinite;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}

.category-filter {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
  margin-bottom: 20px;
  padding: 0 20px;
  max-width: 1800px;
  margin: 0 auto 20px;
}

.category-btn {
  padding: 8px 16px;
  border: none;
  border-radius: 20px;
  background-color: #fff;
  color: #333;
  cursor: pointer;
  transition: all 0.3s;
  font-size: 14px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

.category-btn:hover {
  background-color: #f5f5f5;
  transform: translateY(-2px);
}

.category-btn.active {
  background-color: #1890ff;
  color: white;
}

@media (max-width: 768px) {
  .category-filter {
    padding: 0 10px;
  }
  
  .category-btn {
    padding: 6px 12px;
    font-size: 12px;
  }
}

.header {
  text-align: center;
  margin-bottom: 30px;
  padding: 20px;
  background: linear-gradient(135deg, #1890ff 0%, #722ED1 100%);
  color: white;
  border-radius: 12px;
  max-width: 1800px;
  margin: 0 auto 30px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.1);
}

.header h1 {
  margin: 0;
  font-size: 2.5em;
  font-weight: bold;
  background: linear-gradient(to right, #fff, #e0e0e0);
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.header p {
  margin: 10px 0 0;
  font-size: 1.2em;
  opacity: 0.9;
}

@media (max-width: 768px) {
  .header {
    padding: 15px;
    margin-bottom: 20px;
  }
  
  .header h1 {
    font-size: 2em;
  }
  
  .header p {
    font-size: 1em;
  }
}
</style>

    padding: 10px;