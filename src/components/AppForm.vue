<template>
  <form class="card card-w30" @submit.prevent="addComponent">
    <div class="form-control">
      <label for="type">Тип блока</label>
      <select id="type" v-model="type">
        <option value="title">Заголовок</option>
        <option value="subtitle">Подзаголовок</option>
        <option value="avatar">Аватар</option>
        <option value="text">Текст</option>
      </select>
    </div>

    <div class="form-control">
      <label for="value">Значение</label>
      <textarea id="value" v-model="value" rows="3"></textarea>
      <span v-if="this.error" class="error-msg">{{ this.error }}</span>
    </div>

    <button class="btn primary" :disabled="!(value.length > 3)">Добавить</button>
  </form>
</template>

<script>
export default {
  name: 'AppForm',
  data() {
    return {
      type: 'title',
      value: '',
      error: null
    }
  },
  methods: {
    isFormValid() {
      if (!this.value.length) {
        this.error = 'Введите значение'
        return false
      }

      if (this.type === 'avatar' && this.value.match(/\.(jpeg|jpg|gif|png)$/) === null) {
        this.error = 'URL указан неверно'
        return false
      }

      return true
    },

    addComponent() {
      if (!this.isFormValid()) return

      this.$emit('formData', {
        type: this.type,
        value: this.value
      })

      this.error = null
      this.value = ''
      this.type = 'title'
    }
  }
}
</script>

<style scoped>
  .error-msg {
    display: block;
    margin: 5px 0 15px;
    color:red;
    font-size: 15px;
  }
</style>
