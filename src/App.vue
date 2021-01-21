<template>
  <div class="container column">
    <app-sidebar @send-block="logParams"></app-sidebar>
    <app-view :blocks="blocks"></app-view>
  </div>
  <div class="container">
    <p>
      <button
        class="btn primary"
        @click="getComments"
      >Загрузить комментарии
      </button>
    </p>
    <app-comments v-if="comments.length > 0" :comments="comments"></app-comments>
    <div class="card" v-if="err !== ''">{{err}}</div>
    <div class="loader" v-if="loader"></div>
  </div>
</template>

<script>
import AppComments from '@/components/AppComments'
import AppSidebar from '@/components/AppSidebar'
import AppView from '@/components/AppView'

export default {
  data () {
    return {
      blocks: [],
      comments: {},
      loader: false,
      err: ''
    }
  },
  methods: {
    logParams (content, type) {
      this.blocks.push({ type, content })
    },
    async getComments () {
      try {
        this.loader = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
        if (response.ok) {
          this.comments = await response.json()
        } else {
          throw new Error('Not response, STATUS:', response.status)
        }
        this.loader = false
      } catch (e) {
        this.loader = false
        this.err = 'Мы не смогли получить комментарии. Обратитесь к Администрации сайта.'
        console.error('An error occurred while getting data in ' + 'App.vue; ' + 'func: getComments; MESSAGE:', e.message)
      }
    }
  },
  components: {
    AppSidebar,
    AppComments,
    AppView
  }
}
</script>

<style>
.avatar {
  display: flex;
  justify-content: center;
}

.avatar img {
  width: 150px;
  height: auto;
  border-radius: 50%;
}
</style>
