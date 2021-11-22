<template>
  <div class="container column">

    <AppForm />

    <div class="card card-w70">
      <component
        v-if="currentComponent"
        :is="currentComponent"
      >
      </component>
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <AppComments />
</template>

<script>
import AppForm from './components/AppForm'
import AppComments from './components/AppComments'

export default {
  name: 'App',
  components: {
    AppForm,
    AppComments
  },
  data() {
    return {
      currentComponent: null
    }
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
