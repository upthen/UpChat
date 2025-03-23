<template>
  <div class="up-slot-container">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
import { defineOptions } from 'vue'
defineOptions({
  name: 'UpSlot',
})
import { defineProps } from 'vue'
const props = defineProps<{}>()
// 组件逻辑
</script>

<style scoped lang="scss">
/* 组件样式 */
.up-slot-container {
  width: auto;
  height: 100%;
}
</style>
