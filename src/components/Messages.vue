<template>
  <div>
    <MessageItem v-for="message in data" :key="message.id" :message="message" />
  </div>
</template>

<script>
import MessageItem from '@/components/MessageItem'
export default {
  name: 'Messages',
  components: {
    MessageItem
  },
  props: {
    data: {
      type: [Array, Object],
      default: () => []
    }
  }
}
</script>
