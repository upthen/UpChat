<template>
  <div class="container">
    <div ref="messageContainer" class="message-area">
      <up-chat-item v-for="item in messages" :key="item.key" :position="item.position">
        <up-bubble v-if="item.type === 'text'" :class="item.position" :content="item.content" />
        <up-slot v-else-if="item.type === 'slot'">
          <component :is="item.content.name" v-bind="item.content.props" />
        </up-slot>
      </up-chat-item>
    </div>
    <UpSender type="input_select" @send="handleSend" :option="['头疼', '鼻塞', '发烧']" />
  </div>
</template>

<script setup lang="ts">
import {
  UpBubble,
  UpSender,
  UpChatItem,
  UpIntro,
  UpInput,
  UpContent,
  UpSlot,
  UpAction,
  UpPrompt,
  UpSuggestion,
} from './components/index'
import { ref, nextTick } from 'vue'
import UpCard from './views/UpCard.vue'

type MessageType = {
  key: symbol
  type: 'text' | 'image' | 'audio' | 'video' | 'file' | 'location' | 'link' | 'slot'
  position: 'left' | 'right' | 'center'
  content: string | object
  time?: string
}

/**
 *
 */
const messages = ref<Array<MessageType>>([
  {
    key: Symbol(),
    type: 'text',
    position: 'left',
    content: '角色1：这是第1条消息',
    time: new Date().toLocaleTimeString(),
  },
  {
    key: Symbol(),
    type: 'text',
    position: 'right',
    content: '角色2：这是第2条消息',
    time: new Date().toLocaleTimeString(),
  },
  {
    key: Symbol(),
    type: 'text',
    position: 'left',
    content: '角色1：这是第3条消息',
    time: new Date().toLocaleTimeString(),
  },
  {
    key: Symbol(),
    type: 'slot',
    position: 'center',
    content: {
      name: UpCard,
      props: {
        title: '这是一个卡片',
        content: '这是一个卡片的内容',
      },
      component: UpCard,
    },
    time: new Date().toLocaleTimeString(),
  },
  {
    key: Symbol(),
    type: 'slot',
    position: 'left',
    content: {
      name: UpCard,
      props: {
        title: '这是一个卡片',
        content: '这是一个卡片的内容',
      },
      component: UpCard,
    },
    time: new Date().toLocaleTimeString(),
  },
  {
    key: Symbol(),
    type: 'slot',
    position: 'right',
    content: {
      name: UpCard,
      props: {
        title: '这是一个卡片',
        content: '这是一个卡片的内容',
      },
      component: UpCard,
    },
    time: new Date().toLocaleTimeString(),
  },
])

const messageContainer = ref<HTMLElement | null>(null)

const randomReplies = [
  '收到您的消息，正在处理中',
  '已记录您的要求',
  '我们稍后会回复您',
  '正在查询相关信息',
  '请稍等片刻',
]

const handleSend = (text: string) => {
  // 添加用户消息
  messages.value.push({
    position: 'right',
    content: text,
    time: new Date().toLocaleTimeString(),
    type: 'text',
    key: Symbol(),
  })

  // 添加模拟回复
  messages.value.push({
    position: 'left',
    content: randomReplies[Math.floor(Math.random() * randomReplies.length)],
    time: new Date().toLocaleTimeString(),
    type: 'text',
    key: Symbol(),
  })

  nextTick(() => {
    if (messageContainer.value) {
      messageContainer.value.scrollTop = messageContainer.value.scrollHeight
    }
  })
}
// 在 <script setup> 中添加以下内容，将组件挂载到全局
</script>
<style scoped lang="scss">
.container {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
}
.UpBubble {
  background-color: #f0f0f0;
  border-radius: 10px;
  padding: 10px;
  margin: 10px;
  max-width: 80%;
  color: #333;
}
.left {
  align-self: flex-start;
}
.right {
  align-self: flex-end;
}
.message-area {
  flex: 1;
  overflow-y: auto;
  width: 100%;
  padding: 20px;
  box-sizing: border-box;
  max-height: calc(100vh - 120px);
  scroll-behavior: smooth;
}

.container {
  height: 100vh;
  display: flex;
  flex-direction: column;
}
</style>
