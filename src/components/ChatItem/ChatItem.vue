<template>
  <div class="chat__item" :class="`chat__item--${props.position}`">
    <slot></slot>
  </div>
</template>

<script setup lang="ts">
defineOptions({
  name: 'UpChatItem',
})
const props = defineProps<{
  position?: 'left' | 'right' | 'center'
}>()
// 这里可以添加组件的逻辑
</script>

<style scoped lang="scss">
.chat {
  &__item {
    width: 100%;
    display: flex;
    padding: 16px 16px;

    &--left {
      justify-content: flex-start;
    }

    &--right {
      justify-content: flex-end;
    }

    &--center {
      justify-content: center;
    }
  }
}
</style>
