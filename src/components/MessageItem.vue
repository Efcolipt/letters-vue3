<template>
  <div class="message">
    <div class="info">
      <time class="time" :datetime="message.date">{{ message.date }}</time>
      <p class="author-paragraph">/<span class="author">{{ message.authorName }}</span> /</p>
      <p class="url">{{ message.authorUrl }}</p>
    </div>
    <p v-html="message.markedContent"></p>
  </div>
</template>

<script>
export default {
  name: 'MessageItem',
  props: {
    message: {
      type: [Array, Object],
      default: () => []
    }
  }
}
</script>

<style scoped>
  .message{
    padding:10px;
    margin:10px;
    max-width: 950px;
    margin: 0 auto;
  }
  .message p{
    margin:10px 0;
    font-size: 18px;
  }
  .info{
    display: flex;
    align-items: center;
  }
  .author{
    font-size: 20px;
    margin: 0 5px!important;
  }
  .time,.url{
    margin: 0 5px!important;
  }
  .author-paragraph{
    margin: 0 5px!important;
  }
</style>
