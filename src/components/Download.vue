<template>
  <div class="download">
      <div v-if="!loading">
        <button  @click="$emit('download')">
            Загрузить еще
        </button>
      </div>
      <div v-else>
        <p >Загружаем данные</p>
      </div>
  </div>
</template>

<script>
export default {
  name: 'Download',
  props: {
    loading: {
      type: Boolean,
      default: false
    }
  }
}
</script>

<style scoped>
  .download{
    padding: 10px;
    margin: 10px;
    text-align: center;
  }
</style>
