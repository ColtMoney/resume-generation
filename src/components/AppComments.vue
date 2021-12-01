<template>
  <div class="container">
    <p>
      <button
        v-if="!commentsItems.length"
        class="btn primary"
        @click="uploadComments"
      >
        Загрузить комментарии
      </button>
    </p>
    <div v-if="commentsItems.length" class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <AppCommentItem v-for="item in commentsItems" :key="item.id" :comment="item" />
      </ul>
    </div>
    <div v-if="isLoading" class="loader"></div>
  </div>
</template>

<script>
import AppCommentItem from './AppCommentItem'
export default {
  name: 'AppComments',
  components: {
    AppCommentItem
  },
  data() {
    return {
      isLoading: false,
      commentsItems: []
    }
  },
  methods: {
    async fetchComments() {
      try {
        this.isLoading = true
        const response = await fetch('https://jsonplaceholder.typicode.com/comments?_limit=42')
        const data = await response.json()
        this.commentsItems = data
        this.isLoading = false
      } catch (e) {
        this.isLoading = false
        throw new Error(e.message)
      }
    },
    uploadComments() {
      this.fetchComments()
    }
  }
}
</script>

<style scoped>

</style>
