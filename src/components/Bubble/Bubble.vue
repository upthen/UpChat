<template>
  <div class="bubble-container" :class="role">
    <img :src="avatar || defaultAvatar" alt="Avatar" class="avatar" />
    <div class="bubble" :style="{ backgroundColor: getBubbleColor() }">
      <div class="time">{{ time }}</div>
      <div>{{ content }}</div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { defineOptions, defineProps } from 'vue'
const props = defineProps<{
  content: string
  role: string
  avatar?: string
  time: string
}>()
const defaultAvatar = '/src/assets/logo.svg'
const getBubbleColor = () => {
  return props.role === 'left' ? '#e0f7fa' : '#f0f0f0'
}
defineOptions({
  name: 'UpBubble',
})
// 组件逻辑
</script>

<style scoped lang="scss">
.bubble-container {
  display: flex;
  align-items: flex-start;
  padding: 8px 12px;
  column-gap: 10px;
}
.avatar {
  width: 30px;
  height: 30px;
  border-radius: 50%;
}
.bubble {
  border-radius: 8px;
  padding: 8px 12px;
  max-width: 75%;
  word-wrap: break-word;
  color: black;
}
.time {
  font-size: 12px;
  color: #999;
  margin-bottom: 4px;
}
.left {
  flex-direction: row;
}

.right {
  flex-direction: row-reverse;
}
</style>
