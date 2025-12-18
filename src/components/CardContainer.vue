<template>
  <div id="card-container" class="card-container" :style="containerStyle">
    <!-- 生日贺卡 -->
    <div 
      v-if="template === 'birthday'" 
      class="card birthday-card" 
      :class="{ flipped: isFlipped }"
      @click="handleCardClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <div class="card-inner">
        <div class="card-front">
          <div class="card-decoration">
            <div class="birthday-cake">🎂</div>
            <div class="confetti">
              <div 
                v-for="i in confettiCount" 
                :key="`confetti-${i}`"
                class="confetti-piece"
                :style="getConfettiStyle(i)"
              ></div>
            </div>
            <!-- 新增气泡装饰 -->
            <div class="bubbles">
              <div 
                v-for="i in bubbleCount" 
                :key="`bubble-${i}`"
                class="bubble"
                :style="getBubbleStyle(i)"
              >💭</div>
            </div>
          </div>
          <h2>生日快乐！</h2>
          <p>点击打开贺卡</p>
        </div>
        <div class="card-back">
          <h3>祝你生日快乐！</h3>
          <p>愿你的每一天都充满快乐和惊喜！</p>
          <div class="card-signature">🎁 来自神秘朋友</div>
        </div>
      </div>
    </div>
    
    <!-- 节日贺卡 -->
    <div 
      v-if="template === 'holiday'" 
      class="card holiday-card" 
      :class="{ flipped: isFlipped }"
      @click="handleCardClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <div class="card-inner">
        <div class="card-front">
          <div class="card-decoration">
            <div class="christmas-tree">🎄</div>
            <div class="snowflakes">
              <div 
                v-for="i in snowflakeCount" 
                :key="`snowflake-${i}`"
                class="snowflake"
                :style="getSnowflakeStyle(i)"
              >❄️</div>
            </div>
            <!-- 新增星星装饰 -->
            <div class="stars">
              <div 
                v-for="i in starCount" 
                :key="`star-${i}`"
                class="star"
                :style="getStarStyle(i)"
              >⭐</div>
            </div>
          </div>
          <h2>节日快乐！</h2>
          <p>点击打开贺卡</p>
        </div>
        <div class="card-back">
          <h3>节日快乐！</h3>
          <p>愿这个节日充满爱与温暖！</p>
          <div class="card-signature">🎄 来自神秘朋友</div>
        </div>
      </div>
    </div>
    
    <!-- 感谢贺卡 -->
    <div 
      v-if="template === 'thankyou'" 
      class="card thankyou-card" 
      :class="{ flipped: isFlipped }"
      @click="handleCardClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <div class="card-inner">
        <div class="card-front">
          <div class="card-decoration">
            <div class="thankyou-icon">🙏</div>
            <div class="hearts">
              <div 
                v-for="i in heartCount" 
                :key="`heart-${i}`"
                class="heart"
                :style="getHeartStyle(i)"
              >❤️</div>
            </div>
            <!-- 新增花瓣装饰 -->
            <div class="petals">
              <div 
                v-for="i in petalCount" 
                :key="`petal-${i}`"
                class="petal"
                :style="getPetalStyle(i)"
              >🌸</div>
            </div>
          </div>
          <h2>感谢有你！</h2>
          <p>点击打开贺卡</p>
        </div>
        <div class="card-back">
          <h3>非常感谢！</h3>
          <p>感谢你一直以来的支持和帮助！</p>
          <div class="card-signature">🙏 来自神秘朋友</div>
        </div>
      </div>
    </div>
    
    <!-- 爱情贺卡 -->
    <div 
      v-if="template === 'love'" 
      class="card love-card" 
      :class="{ flipped: isFlipped }"
      @click="handleCardClick"
      @touchstart="handleTouchStart"
      @touchmove="handleTouchMove"
      @touchend="handleTouchEnd"
    >
      <div class="card-inner">
        <div class="card-front">
          <div class="card-decoration">
            <div class="love-hearts">❤️</div>
            <div class="sparkles">
              <div 
                v-for="i in sparkleCount" 
                :key="`sparkle-${i}`"
                class="sparkle"
                :style="getSparkleStyle(i)"
              >✨</div>
            </div>
            <!-- 新增萤火虫装饰 -->
            <div class="fireflies">
              <div 
                v-for="i in fireflyCount" 
                :key="`firefly-${i}`"
                class="firefly"
                :style="getFireflyStyle(i)"
              >🪲</div>
            </div>
          </div>
          <h2>爱你哟！</h2>
          <p>点击打开贺卡</p>
        </div>
        <div class="card-back">
          <h3>亲爱的，</h3>
          <p>你是我生命中最美好的礼物！</p>
          <div class="card-signature">❤️ 来自神秘爱人</div>
        </div>
      </div>
    </div>
    
    <!-- 返回按钮 -->
    <button class="back-btn" @click="handleBack" aria-label="返回选择模板">
      ← 返回
    </button>
    
    <!-- 音乐控制按钮 -->
    <button 
      class="music-control-btn" 
      @click="toggleMusic" 
      :aria-label="isMusicPlaying ? '暂停音乐' : '播放音乐'"
      :title="isMusicPlaying ? '暂停音乐' : '播放音乐'"
    >
      {{ isMusicPlaying ? '🔇' : '🔊' }}
    </button>
    
    <!-- 分享按钮 -->
    <button 
      class="share-btn" 
      @click="shareCard" 
      aria-label="分享贺卡"
      title="分享贺卡"
    >
      📤
    </button>
  </div>
  
  <!-- 提示弹窗层 -->
  <div id="popup-layer" aria-live="polite" aria-atomic="false">
    <div 
      v-for="popup in popups" 
      :key="popup.id"
      class="popup"
      :class="{ 'fade-out': popup.isFading }"
    >
      {{ popup.message }}
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted, onUnmounted, watch } from 'vue'

// 定义组件的属性和事件
const props = defineProps({
  template: {
    type: String,
    required: true,
    validator: (value) => ['birthday', 'holiday', 'thankyou', 'love'].includes(value)
  }
})

const emit = defineEmits(['back'])

// 贺卡翻页状态
const isFlipped = ref(false)

// 装饰元素数量 - 减少数量以提高性能
const confettiCount = ref(15)
const snowflakeCount = ref(10)
const heartCount = ref(12)
const sparkleCount = ref(20)
// 新增装饰元素
const bubbleCount = ref(8)
const starCount = ref(15)
const petalCount = ref(12)
const fireflyCount = ref(10)

// 音频状态
const isMusicPlaying = ref(false)
const bgMusic = ref(null)
const flipSound = ref(null)

// 触摸事件处理
const touchStartX = ref(0)
const touchStartY = ref(0)
const isTouching = ref(false)

// 提示弹窗
const popups = ref([])
let popupId = 0

// 容器样式
const containerStyle = computed(() => {
  switch (props.template) {
    case 'birthday':
      return { background: 'linear-gradient(135deg, #f5f7fa 0%, #ffccbc 50%, #ffe082 100%)' }
    case 'holiday':
      return { background: 'linear-gradient(135deg, #e3f2fd 0%, #b2ebf2 50%, #80deea 100%)' }
    case 'thankyou':
      return { background: 'linear-gradient(135deg, #e8f5e9 0%, #d4edda 50%, #c8e6c9 100%)' }
    case 'love':
      return { background: 'linear-gradient(135deg, #fce4ec 0%, #f8bbd0 50%, #ffcdd2 100%)' }
    default:
      return { background: 'linear-gradient(135deg, #f5f7fa 0%, #c3cfe2 100%)' }
  }
})

// 根据屏幕尺寸调整装饰元素数量
const adjustDecorationCount = () => {
  const width = window.innerWidth
  let countRatio = 1
  
  if (width < 375) {
    countRatio = 0.6
  } else if (width < 640) {
    countRatio = 0.8
  } else if (width < 1024) {
    countRatio = 1
  } else {
    countRatio = 1.2
  }
  
  // 使用减少后的基数，减少渲染负担
  confettiCount.value = Math.floor(15 * countRatio)
  snowflakeCount.value = Math.floor(10 * countRatio)
  heartCount.value = Math.floor(12 * countRatio)
  sparkleCount.value = Math.floor(20 * countRatio)
  // 新增装饰元素
  bubbleCount.value = Math.floor(8 * countRatio)
  starCount.value = Math.floor(15 * countRatio)
  petalCount.value = Math.floor(12 * countRatio)
  fireflyCount.value = Math.floor(10 * countRatio)
}

// 初始化音频
const initAudio = () => {
  // 背景音乐
  bgMusic.value = new Audio('https://sf5-hl-cdn-tos.douyinstatic.com/obj/ies-music/7538982702662699786.mp3')
  bgMusic.value.volume = 0.3
  bgMusic.value.preload = 'metadata'
  bgMusic.value.loop = true
  
  // 翻页音效
  flipSound.value = new Audio('https://assets.mixkit.co/active_storage/sfx/2167/2167-preview.mp3')
  flipSound.value.volume = 0.5
  flipSound.value.preload = 'metadata'
}

// 播放背景音乐
const playBackgroundMusic = async () => {
  if (!bgMusic.value) return
  
  try {
    await bgMusic.value.play()
    isMusicPlaying.value = true
  } catch (err) {
    console.log('自动播放失败，需要用户交互后才能播放:', err)
    showPopup('点击贺卡或音乐按钮即可播放音乐')
  }
}

// 切换音乐播放状态
const toggleMusic = () => {
  if (!bgMusic.value) return
  
  if (bgMusic.value.paused) {
    bgMusic.value.play().catch(err => {
      console.log('播放失败:', err)
      showPopup('播放音乐失败，请检查网络连接。')
    })
    isMusicPlaying.value = true
  } else {
    bgMusic.value.pause()
    isMusicPlaying.value = false
  }
}

// 播放翻页音效
const playFlipSound = () => {
  if (!flipSound.value) return
  
  flipSound.value.currentTime = 0
  flipSound.value.play().catch(err => console.log('播放翻页音效失败:', err))
}

// 贺卡翻页处理
const handleCardClick = () => {
  isFlipped.value = !isFlipped.value
  playFlipSound()
  
  // 如果是第一次点击，播放音乐
  if (!isMusicPlaying.value) {
    playBackgroundMusic()
  }
}

// 触摸事件处理
const handleTouchStart = (e) => {
  isTouching.value = true
  touchStartX.value = e.touches[0].clientX
  touchStartY.value = e.touches[0].clientY
  
  // 给卡片添加按下效果
  e.currentTarget.style.transform = 'scale(0.98)'
}

const handleTouchMove = (e) => {
  if (!isTouching.value) return
  // 防止页面滚动干扰
  e.preventDefault()
}

const handleTouchEnd = (e) => {
  if (!isTouching.value) return
  
  isTouching.value = false
  const touchEndX = e.changedTouches[0].clientX
  const touchEndY = e.changedTouches[0].clientY
  const deltaX = touchEndX - touchStartX.value
  const deltaY = touchEndY - touchStartY.value
  
  // 恢复卡片原状态
  e.currentTarget.style.transform = ''
  
  // 判断滑动方向
  if (Math.abs(deltaX) > Math.abs(deltaY) && Math.abs(deltaX) > 50) {
    // 水平滑动超过50px
    if (deltaX > 0) {
      // 向右滑动 - 翻回正面
      if (isFlipped.value) {
        isFlipped.value = false
        playFlipSound()
      }
    } else {
      // 向左滑动 - 翻到背面
      if (!isFlipped.value) {
        isFlipped.value = true
        playFlipSound()
      }
    }
  } else {
    // 点击或垂直滑动，使用默认的点击翻转逻辑
    handleCardClick()
  }
}

// 分享功能
const shareCard = () => {
  if (navigator.share) {
    navigator.share({
      title: '神秘贺卡',
      text: '我收到了一张神秘贺卡，快来看看吧！',
      url: window.location.href
    })
    .then(() => console.log('分享成功'))
    .catch((error) => console.log('分享失败:', error))
  } else {
    // 复制链接到剪贴板
    navigator.clipboard.writeText(window.location.href)
      .then(() => {
        showPopup('链接已复制到剪贴板！')
      })
      .catch((error) => {
        console.error('复制失败:', error)
        showPopup('分享功能不可用，请手动复制链接。')
      })
  }
}

// 显示提示弹窗
const showPopup = (message) => {
  const id = popupId++
  const popup = { id, message, isFading: false }
  popups.value.push(popup)
  
  // 3秒后自动移除
  setTimeout(() => {
    popup.isFading = true
    setTimeout(() => {
      popups.value = popups.value.filter(p => p.id !== id)
    }, 300)
  }, 3000)
}

// 装饰元素样式生成
const getConfettiStyle = (index) => {
  const random = Math.random()
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 3}s`,
    animationDuration: `${Math.random() * 2 + 2}s`,
    transform: `rotate(${Math.random() * 360}deg)`,
    width: `${Math.random() * 8 + 8}px`,
    height: `${Math.random() * 20 + 20}px`,
    opacity: `${Math.random() * 0.5 + 0.5}`
  }
}

const getSnowflakeStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 5}s`,
    animationDuration: `${Math.random() * 3 + 5}s`,
    fontSize: `${Math.random() * 20 + 10}px`,
    opacity: `${Math.random() * 0.5 + 0.5}`
  }
}

const getHeartStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 2}s`,
    animationDuration: `${Math.random() * 2 + 3}s`,
    fontSize: `${Math.random() * 15 + 10}px`,
    opacity: `${Math.random() * 0.5 + 0.5}`
  }
}

const getSparkleStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 1}s`,
    animationDuration: `${Math.random() * 1 + 2}s`,
    fontSize: `${Math.random() * 15 + 8}px`,
    opacity: `${Math.random() * 0.5 + 0.5}`
  }
}

// 新增装饰元素样式生成函数
const getBubbleStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 3}s`,
    animationDuration: `${Math.random() * 3 + 4}s`,
    fontSize: `${Math.random() * 30 + 15}px`,
    opacity: `${Math.random() * 0.3 + 0.3}`
  }
}

const getStarStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 5}s`,
    animationDuration: `${Math.random() * 4 + 6}s`,
    fontSize: `${Math.random() * 15 + 10}px`,
    opacity: `${Math.random() * 0.6 + 0.4}`
  }
}

const getPetalStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 4}s`,
    animationDuration: `${Math.random() * 3 + 5}s`,
    fontSize: `${Math.random() * 20 + 15}px`,
    opacity: `${Math.random() * 0.5 + 0.5}`
  }
}

const getFireflyStyle = (index) => {
  return {
    left: `${Math.random() * 100}%`,
    animationDelay: `${Math.random() * 2}s`,
    animationDuration: `${Math.random() * 4 + 5}s`,
    fontSize: `${Math.random() * 10 + 8}px`,
    opacity: `${Math.random() * 0.6 + 0.4}`
  }
}

// 返回按钮处理
const handleBack = () => {
  emit('back')
}

// 监听页面可见性变化时处理音频
const handleVisibilityChange = () => {
  if (!bgMusic.value) return
  
  if (document.hidden && isMusicPlaying.value) {
    bgMusic.value.pause()
  } else if (!document.hidden && !bgMusic.value.paused) {
    bgMusic.value.play().catch(err => console.log('恢复播放失败:', err))
  }
}

// 生命周期钩子
onMounted(() => {
  initAudio()
  adjustDecorationCount()
  window.addEventListener('resize', adjustDecorationCount)
  document.addEventListener('visibilitychange', handleVisibilityChange)
})

onUnmounted(() => {
  window.removeEventListener('resize', adjustDecorationCount)
  document.removeEventListener('visibilitychange', handleVisibilityChange)
  
  // 清理音频资源
  if (bgMusic.value) {
    bgMusic.value.pause()
    bgMusic.value = null
  }
  
  if (flipSound.value) {
    flipSound.value = null
  }
})
</script>

<style scoped>
.card-container {
  width: 100%;
  height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 20px;
  position: relative;
  overflow: hidden;
}

.card {
  width: 100%;
  max-width: 400px;
  height: 600px;
  perspective: 1000px;
  cursor: pointer;
  user-select: none;
}

.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.6s ease;
  transform-style: preserve-3d;
  box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
  border-radius: 12px;
}

.card.flipped .card-inner {
  transform: rotateY(180deg);
}

.card-front, .card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  -webkit-backface-visibility: hidden;
  backface-visibility: hidden;
  border-radius: 12px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  padding: 30px;
}

.card-front {
  background-color: white;
  color: var(--text);
}

.card-back {
  background-color: white;
  color: var(--text);
  transform: rotateY(180deg);
}

.card-decoration {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
  pointer-events: none;
}

.birthday-cake, .christmas-tree, .thankyou-icon, .love-hearts {
  font-size: 80px;
  margin-bottom: 20px;
  position: relative;
  z-index: 1;
}

/* 彩纸动画 */
.confetti {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.confetti-piece {
  position: absolute;
  top: -10%;
  background-color: var(--birthday-primary);
  animation: confetti-fall linear infinite;
  will-change: transform, opacity;
}

/* 雪花动画 */
.snowflakes {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.snowflake {
  position: absolute;
  top: -10%;
  color: white;
  text-shadow: 0 0 5px rgba(0, 0, 0, 0.3);
  animation: snowfall linear infinite;
  will-change: transform, opacity;
}

/* 爱心动画 */
.hearts {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.heart {
  position: absolute;
  top: -10%;
  color: var(--thankyou-primary);
  animation: heart-float linear infinite;
  will-change: transform, opacity;
}

/* 火花动画 */
.sparkles {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  overflow: hidden;
}

.sparkle {
  position: absolute;
  top: -10%;
  color: gold;
  text-shadow: 0 0 5px rgba(255, 215, 0, 0.5);
  animation: sparkle-float linear infinite;
  will-change: transform, opacity;
}

/* 卡片标题和内容 */
.card h2 {
  font-size: 32px;
  font-weight: 800;
  margin-bottom: 10px;
  position: relative;
  z-index: 1;
}

.card-back h3 {
  font-size: 28px;
  font-weight: 800;
  margin-bottom: 20px;
  position: relative;
  z-index: 1;
}

.card p {
  font-size: 18px;
  margin-bottom: 20px;
  position: relative;
  z-index: 1;
}

.card-signature {
  margin-top: auto;
  font-size: 14px;
  color: var(--subtext);
  position: relative;
  z-index: 1;
}

/* 控制按钮 */
.back-btn, .music-control-btn, .share-btn {
  position: fixed;
  bottom: 20px;
  border: none;
  border-radius: 50%;
  width: 56px;
  height: 56px;
  font-size: 20px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  box-shadow: var(--shadow-heavy);
  transition: all 0.2s ease;
  background-color: white;
  color: var(--text);
}

.back-btn:hover, .music-control-btn:hover, .share-btn:hover {
  transform: translateY(-2px);
  box-shadow: 0 24px 56px rgba(0,0,0,0.2);
}

.back-btn {
  left: 20px;
  font-size: 14px;
  font-weight: 600;
  border-radius: 28px;
  width: auto;
  padding: 0 20px;
}

.music-control-btn {
  right: 20px;
}

.share-btn {
  right: 90px;
}

/* 提示弹窗 */
.popup {
  position: fixed;
  top: 20px;
  left: 50%;
  transform: translateX(-50%);
  background-color: rgba(0, 0, 0, 0.8);
  color: white;
  padding: 12px 24px;
  border-radius: 4px;
  font-size: 16px;
  z-index: 1000;
  animation: fade-in 0.3s ease-out;
}

.popup.fade-out {
  animation: fade-out 0.3s ease-out forwards;
}

/* 动画关键帧 */
@keyframes confetti-fall {
  0% {
    transform: translateY(-10vh) rotate(0deg);
    opacity: 1;
  }
  100% {
    transform: translateY(100vh) rotate(360deg);
    opacity: 0;
  }
}

@keyframes snowfall {
  0% {
    transform: translateY(-10vh) translateX(0);
    opacity: 1;
  }
  50% {
    transform: translateY(50vh) translateX(50px);
    opacity: 0.8;
  }
  100% {
    transform: translateY(100vh) translateX(-50px);
    opacity: 0;
  }
}

@keyframes heart-float {
  0% {
    transform: translateY(-10vh) scale(1);
    opacity: 1;
  }
  50% {
    transform: translateY(50vh) scale(1.2);
    opacity: 0.8;
  }
  100% {
    transform: translateY(100vh) scale(0.8);
    opacity: 0;
  }
}

@keyframes sparkle-float {
  0% {
    transform: translateY(-10vh) rotate(0deg);
    opacity: 1;
  }
  25% {
    transform: translateY(25vh) rotate(90deg);
    opacity: 0.8;
  }
  50% {
    transform: translateY(50vh) rotate(180deg);
    opacity: 1;
  }
  75% {
    transform: translateY(75vh) rotate(270deg);
    opacity: 0.8;
  }
  100% {
    transform: translateY(100vh) rotate(360deg);
    opacity: 0;
  }
}

@keyframes fade-in {
  from { opacity: 0; transform: translateX(-50%) translateY(-10px); }
  to { opacity: 1; transform: translateX(-50%) translateY(0); }
}

@keyframes fade-out {
  from { opacity: 1; transform: translateX(-50%) translateY(0); }
  to { opacity: 0; transform: translateX(-50%) translateY(-10px); }
}

/* 响应式设计 */
@media (max-width: 768px) {
  .card {
    height: 500px;
  }
  
  .card h2 {
    font-size: 28px;
  }
  
  .card-back h3 {
    font-size: 24px;
  }
  
  .card p {
    font-size: 16px;
  }
  
  .birthday-cake, .christmas-tree, .thankyou-icon, .love-hearts {
    font-size: 60px;
  }
  
  .back-btn, .music-control-btn, .share-btn {
    width: 48px;
    height: 48px;
    font-size: 18px;
  }
  
  .back-btn {
    font-size: 13px;
  }
}

@media (max-width: 480px) {
  .card {
    height: 400px;
    max-width: 320px;
  }
  
  .card h2 {
    font-size: 24px;
  }
  
  .card-back h3 {
    font-size: 20px;
  }
  
  .card p {
    font-size: 14px;
  }
  
  .birthday-cake, .christmas-tree, .thankyou-icon, .love-hearts {
    font-size: 50px;
  }
}
</style>