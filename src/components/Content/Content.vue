<template>
  <div>这是一个内容组件</div>
</template>

<script setup lang="ts">
import { defineOptions } from 'vue'
import { defineProps } from 'vue'
const props = defineProps<{}>()
defineOptions({
  name: 'UpContent',
})
// 组件逻辑
</script>

<style scoped lang="scss">
/* 组件样式 */
</style>
