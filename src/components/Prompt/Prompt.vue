<template>
  <div>这是一个提示词组件</div>
</template>

<script setup lang="ts">
import { defineOptions } from 'vue'
import { defineProps } from 'vue'
const props = defineProps<{}>()
defineOptions({
  name: 'UpPrompt',
})
// 组件逻辑
</script>

<style scoped lang="scss">
/* 组件样式 */
</style>
