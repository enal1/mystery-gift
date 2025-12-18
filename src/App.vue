<template>
  <div id="app">
    <!-- 页面加载指示器 -->
    <LoadingIndicator v-if="isLoading" />
    
    <!-- 贺卡模板选择弹窗 -->
    <TemplateSelector 
      v-if="showTemplateSelector"
      @select="handleTemplateSelect"
    />
    
    <!-- 贺卡容器 -->
    <CardContainer 
      v-else
      :template="selectedTemplate"
      @back="showTemplateSelector = true"
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import LoadingIndicator from './components/LoadingIndicator.vue'
import TemplateSelector from './components/TemplateSelector.vue'
import CardContainer from './components/CardContainer.vue'

const isLoading = ref(true)
const showTemplateSelector = ref(true)
const selectedTemplate = ref('birthday')

onMounted(() => {
  // 模拟加载过程
  setTimeout(() => {
    isLoading.value = false
  }, 500)
})

const handleTemplateSelect = (template) => {
  selectedTemplate.value = template
  showTemplateSelector.value = false
}
</script>

<style>
/* 全局样式 */
:root {
  --bg: #ffffff;
  --text: #1a1a1a;
  --subtext: #4d4d4d;
  --border: #e5e5e5;
  --shadow: 0 8px 24px rgba(0,0,0,0.12);
  --shadow-heavy: 0 20px 48px rgba(0,0,0,0.16);
  --overlay: rgba(0, 0, 0, 0.4);
  --accent: #0078d4; /* Windows 蓝 */
  /* 贺卡主题色 */
  --birthday-primary: #ff5252;
  --birthday-secondary: #ffe082;
  --birthday-tertiary: #ffccbc;
  --holiday-primary: #00acc1;
  --holiday-secondary: #80deea;
  --holiday-tertiary: #b2ebf2;
  --thankyou-primary: #66bb6a;
  --thankyou-secondary: #ffeeba;
  --thankyou-tertiary: #d4edda;
  --love-primary: #f44336;
  --love-secondary: #ffcdd2;
  --love-tertiary: #f8bbd0;
}

* {
  box-sizing: border-box;
}

html, body {
  height: 100%;
}

body {
  margin: 0;
  background: linear-gradient(135deg, #f0f4f8 0%, #e8eef5 50%, #dfe7f0 100%);
  color: var(--text);
  font-family: "Noto Sans SC", Segoe UI, system-ui, -apple-system, Roboto, Helvetica, Arial, "PingFang SC", "Hiragino Sans GB", "Microsoft YaHei", sans-serif;
  overflow: hidden;
}
</style>