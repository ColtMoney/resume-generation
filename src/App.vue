<template>
  <!-- eslint-disable vue/no-multiple-template-root -->
  <div class="container column">

    <AppForm @formData="componentHundler" />

    <div class="card card-w70">
      <template v-if="components.length">
        <div
          v-for="component in components"
          :key="component.id"
        >
          <component
            :is="component.name"
            v-bind="component.props"
          >
          </component>
        </div>
      </template>
      <h3 v-else>Добавьте первый блок, чтобы увидеть результат</h3>
    </div>
  </div>
  <AppComments />
</template>

<script>
import AppForm from './components/AppForm'
import AppComments from './components/AppComments'
import AppText from './components/AppText'
import AppTitle from './components/AppTitle'
import AppSubTitle from './components/AppSubTitle'
import AppAvatar from './components/AppAvatar'

const FIREBASE_API = 'https://vue-with-http-99c18-default-rtdb.firebaseio.com/components.json'

export default {
  name: 'App',
  components: {
    AppForm,
    AppComments,
    AppAvatar,
    AppText,
    AppTitle,
    AppSubTitle
  },
  data() {
    return {
      components: []
    }
  },
  mounted() {
    this.loadComponents()
  },
  methods: {
    componentHundler({ type, value }) {
      if (type === 'title') {
        this.createComponent('AppTitle', { title: value })
      } else if (type === 'subtitle') {
        this.createComponent('AppSubTitle', { subtitle: value })
      } else if (type === 'avatar') {
        this.createComponent('AppAvatar', { src: value })
      } else if (type === 'text') {
        this.createComponent('AppText', { text: value })
      }
    },
    async createComponent(name, props) {
      const response = await fetch(FIREBASE_API, {
        method: 'POST',
        headers: {
          'Content-Type': 'application/json'
        },
        body: JSON.stringify({
          name,
          props
        })
      })
      const data = await response.json()
      this.components.push({
        id: data.id,
        name,
        props
      })
    },
    async loadComponents() {
      try {
        const response = await fetch(FIREBASE_API)
        const data = await response.json()
        if (!data) return
        this.components = Object.keys(data).map(key => {
          return {
            id: key,
            ...data[key]
          }
        })
      } catch (e) {
        throw new Error(e.message)
      }
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
