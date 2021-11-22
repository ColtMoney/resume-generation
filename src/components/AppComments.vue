<template>
  <div class="container">
    <p>
      <button class="btn primary">Загрузить комментарии</button>
    </p>
    <div v-if="!isLoading" class="card">
      <h2>Комментарии</h2>
      <ul class="list">
        <AppCommentItem />
      </ul>
    </div>
    <div v-else class="loader"></div>
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
  }
}
</script>

<style scoped>

</style>
