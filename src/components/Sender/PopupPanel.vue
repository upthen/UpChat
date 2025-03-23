<template>
  <transition name="slide-up">
    <div v-if="visible" class="popup-panel">
      <div
        class="option-item"
        v-for="(option, index) in options"
        :key="index"
        @click="handleSelect(option)"
      >
        {{ option }}
      </div>
    </div>
  </transition>
</template>

<script setup lang="ts">
import { ref, defineProps, defineEmits } from 'vue'

const props = defineProps<{
  options: string[]
  visible: boolean
}>()

const emit = defineEmits(['select'])

const handleSelect = (value: string) => {
  emit('select', value)
}
</script>

<style scoped>
.popup-panel {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  max-height: 50vh;
  background: white;
  border-radius: 16px 16px 0 0;
  box-shadow: 0 -2px 10px rgba(0, 0, 0, 0.1);
  overflow-y: auto;
  padding: 12px 0;
}

.option-item {
  padding: 16px 24px;
  font-size: 16px;
  color: #333;
  border-bottom: 1px solid #eee;
  transition: background 0.2s;
}

.option-item:active {
  background: #f5f5f5;
}

.slide-up-enter-active {
  transition: transform 0.3s ease-out;
}

.slide-up-leave-active {
  transition: transform 0.2s ease-in;
}

.slide-up-enter-from,
.slide-up-leave-to {
  transform: translateY(100%);
}
</style>
