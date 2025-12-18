<template>
  <div class="loading-indicator">
    <div class="loading-spinner"></div>
    <div class="loading-text">正在准备神秘贺卡...</div>
  </div>
</template>

<script setup>
// LoadingIndicator组件逻辑
</script>

<style scoped>
.loading-indicator {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(255, 255, 255, 0.95);
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  z-index: 9999;
  transition: opacity 0.5s ease-out;
}

.loading-indicator.hidden {
  opacity: 0;
  pointer-events: none;
}

.loading-spinner {
  width: 60px;
  height: 60px;
  border: 4px solid #f0f0f0;
  border-top: 4px solid var(--accent);
  border-radius: 50%;
  animation: spin 1s linear infinite;
  margin-bottom: 16px;
}

.loading-text {
  font-size: 18px;
  color: var(--text);
  font-weight: 600;
}

@keyframes spin {
  0% { transform: rotate(0deg); }
  100% { transform: rotate(360deg); }
}
</style>