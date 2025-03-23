<template>
  <div class="card">
    <h2>{{ props.title }}</h2>
    <p>{{ props.content }}</p>
    <button type="button" @click="handleConfirm" class="confirm-button">确认</button>
    <button type="button" @click="handleCancel" class="cancel-button">取消</button>
  </div>
</template>

<script lang="ts" setup>
defineOptions({
  name: 'UpCard',
})

interface UpCardProps {
  title?: string
  content?: string
}

const props = defineProps<UpCardProps>()

const handleConfirm = () => {
  console.log('确认操作')
}

const handleCancel = () => {
  console.log('取消操作')
}
</script>

<style scoped>
.card {
  border: 1px solid #ccc;
  padding: 20px;
  border-radius: 4px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

button {
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: all 0.3s ease;
  margin: 0 5px;
}

.confirm-button {
  background-color: #2ecc71;
  color: white;
}

.confirm-button:hover {
  background-color: #27ae60;
  transform: scale(1.05);
}

.cancel-button {
  background-color: #e74c3c;
  color: white;
}

.cancel-button:hover {
  background-color: #c0392b;
  transform: scale(1.05);
}
</style>
