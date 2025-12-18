<template>
  <div class="modal-backdrop" aria-hidden="false">
    <div class="modal" role="dialog" aria-modal="true" aria-labelledby="modal-title">
      <div class="titlebar">
        <span class="icon">🎁</span>
        <span class="title" id="modal-title">神秘贺卡</span>
      </div>
      <div class="content">请杨大美女选择一张贺卡：</div>
      <div class="card-templates">
        <div 
          v-for="template in templates" 
          :key="template.type"
          class="card-template"
          :class="{ active: selectedTemplate === template.type }"
          @click="selectedTemplate = template.type"
        >
          <div class="template-icon">{{ template.icon }}</div>
          <div class="template-name">{{ template.name }}</div>
        </div>
      </div>
      <div class="actions">
        <button 
          class="btn primary" 
          id="confirm-btn" 
          type="button" 
          autofocus
          @click="handleConfirm"
        >确定</button>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

// 定义组件的输出事件
const emit = defineEmits(['select'])

// 定义贺卡模板数据
const templates = [
  { type: 'birthday', icon: '🎂', name: '生日贺卡' },
  { type: 'holiday', icon: '🎄', name: '节日贺卡' },
  { type: 'thankyou', icon: '🙏', name: '感谢贺卡' },
  { type: 'love', icon: '❤️', name: '爱情贺卡' }
]

// 当前选中的模板
const selectedTemplate = ref('birthday')

// 确认选择并触发事件
const handleConfirm = () => {
  emit('select', selectedTemplate.value)
}
</script>

<style scoped>
.modal-backdrop {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--overlay);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
  animation: fadeIn 0.3s ease-out;
}

.modal {
  background-color: var(--bg);
  border-radius: 8px;
  box-shadow: var(--shadow-heavy);
  width: 90%;
  max-width: 500px;
  max-height: 90vh;
  overflow: hidden;
  animation: scaleIn 0.3s ease-out;
}

.titlebar {
  display: flex;
  align-items: center;
  padding: 16px;
  background-color: var(--accent);
  color: white;
  font-weight: 600;
}

.titlebar .icon {
  font-size: 24px;
  margin-right: 8px;
}

.content {
  padding: 24px;
  font-size: 18px;
  font-weight: 600;
  text-align: center;
  color: var(--text);
}

.card-templates {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 16px;
  padding: 0 24px 24px;
}

.card-template {
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 20px;
  background-color: #f8f9fa;
  border: 2px solid transparent;
  border-radius: 8px;
  cursor: pointer;
  transition: all 0.2s ease;
}

.card-template:hover {
  background-color: #e9ecef;
  transform: translateY(-2px);
  box-shadow: var(--shadow);
}

.card-template.active {
  border-color: var(--accent);
  background-color: rgba(0, 120, 212, 0.05);
}

.template-icon {
  font-size: 48px;
  margin-bottom: 8px;
}

.template-name {
  font-size: 14px;
  font-weight: 500;
  color: var(--text);
}

.actions {
  display: flex;
  justify-content: center;
  padding: 16px 24px 24px;
}

.btn {
  padding: 12px 24px;
  border: none;
  border-radius: 4px;
  font-size: 16px;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.2s ease;
  min-width: 120px;
}

.btn.primary {
  background-color: var(--accent);
  color: white;
}

.btn.primary:hover {
  background-color: #005a9e;
  transform: translateY(-1px);
  box-shadow: var(--shadow);
}

@keyframes fadeIn {
  from { opacity: 0; }
  to { opacity: 1; }
}

@keyframes scaleIn {
  from { transform: scale(0.95); opacity: 0; }
  to { transform: scale(1); opacity: 1; }
}
</style>