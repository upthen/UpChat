<template>
  <div class="sender-container">
    <div class="input-group">
      <input
        v-if="showInput"
        v-model="message"
        type="text"
        placeholder="输入消息..."
        class="sender-input"
        @keyup.enter="sendMessage"
      />
      <button v-if="showSelect" @click="showPopup = true" class="trigger-button">选择选项</button>
      <PopupPanel :options="options || []" :visible="showPopup" @select="handlePopupSelect" />
    </div>
    <button @click="sendMessage" class="sender-button">发送</button>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

defineOptions({
  name: 'UpSender',
})

const emit = defineEmits(['send'])

const props = defineProps<{
  type?: 'input' | 'select' | 'input_select'
  options?: string[]
}>()

const showPopup = ref(false)

const message = ref('')
const selectedOption = ref('')
const showInput = computed(() => ['input', 'input_select'].includes(props.type || 'input'))
const showSelect = computed(() => ['select', 'input_select'].includes(props.type || 'input'))

const handlePopupSelect = (value: string) => {
  selectedOption.value = value
  showPopup.value = false
  if (props.type === 'select') {
    sendMessage()
  }
}

// 发送消息的函数
const sendMessage = () => {
  let content = ''
  if (props.type === 'select') {
    content = selectedOption.value
  } else {
    content = message.value.trim()
  }

  if (content) {
    emit('send', content)
    message.value = ''
    selectedOption.value = ''
  }
}
</script>

<style scoped>
.sender-container {
  width: 100%;
  display: flex;
  align-items: center;
  background-color: #f5f5f5;
  border-top: 1px solid #ddd;
  padding: 10px;
  box-sizing: border-box;
}

.sender-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  margin-right: 10px;
  outline: none;
}

.sender-button {
  padding: 10px 20px;
  background-color: #007bff;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

.sender-button:hover {
  background-color: #0056b3;
}

.input-group {
  flex: 1;
  display: flex;
  gap: 10px;
}

.sender-select {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
  background-color: white;
  outline: none;
}
</style>
