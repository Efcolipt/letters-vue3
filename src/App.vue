/* eslint-disable no-undef */
<template>
  <div class="container">
    <Messages :data="loadData" />
    <Download @download="download" :loading="loading" />
  </div>
</template>

<script>
import Messages from '@/components/Messages'
import Download from '@/components/Download'
export default {
  name: 'App',
  components: {
    Messages,
    Download
  },
  data () {
    return {
      data: [],
      loadData: [],
      counter: 0,
      limit: 10,
      loading: false
    }
  },
  mounted () {
    this.axios.get('/static/feed.json').then((response) => {
      this.data = response.data
      this.loadData = this.data.slice(this.counter, this.counter + this.limit)
      this.markedContent()
    })
  },
  methods: {
    download () {
      if (this.data.length > this.counter) {
        this.loading = true
        setTimeout(() => {
          this.counter += this.limit
          this.loadData = [
            ...this.loadData,
            ...this.data.slice(this.counter, this.counter + this.limit)
          ]
          this.markedContent()
          this.loading = false
        }, 1500)
      }
    },

    markedContent () {
      for (let i = this.counter; this.loadData.length > i; i++) {
        this.loadData[i].id = Date.now() + i
        this.loadData[i].markedContent = this.loadData[i].content
        const formatter = new Intl.DateTimeFormat('ru', {
          hour: 'numeric',
          minute: 'numeric',
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        })
        this.loadData[i].date = formatter.format(Date.parse(this.loadData[i].date))
        const arr = this.loadData[i].markedContent.split('')
        for (let j = 0; j < this.loadData[i].contentPostTones.length; j++) {
          const pos1 = this.loadData[i].contentPostTones[j].position
          const pos2 = this.loadData[i].contentPostTones[j].length
          const tone = this.loadData[i].contentPostTones[j].tone
          let posEdit = pos1
          let posLength = pos2
          while (posLength) {
            arr[posEdit] = `<mark style="background: ${tone < -0.3 ? '#e61919' : tone <= 0.3 || tone <= -0.3 ? '#e4f053' : tone > 0.3 ? '#0bda51' : ''}">${arr[posEdit]}</mark>`
            posEdit++
            posLength--
          }
        }
        this.loadData[i].markedContent = arr.join('')
      }
    }

  }
}
</script>

<style>
* {
  box-sizing: border-box;
  padding: 0;
  margin: 0;
}
a {
  text-decoration: none;
}
.container {
  max-width: 1280px;
  margin: 0 auto;
}
</style>
