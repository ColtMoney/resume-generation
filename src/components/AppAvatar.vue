<template>
  <div class="avatar" v-if="this.src">
    <img :src="this.src">
  </div>
</template>

<script>
export default {
  name: 'AppAvatar',
  props: ['src']
}
</script>

<style scoped>

</style>
