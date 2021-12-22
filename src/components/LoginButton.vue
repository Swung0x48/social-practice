<template>
  <span class="navbar-nav ms-auto" v-if="!valid">
    <button type="button" class="btn btn-outline-primary mx-2" @click="$router.push('/login')">
      登录
    </button>
    <button type="button" class="btn btn-outline-success mx-2" @click="$router.push('/register')">
      注册
    </button>
  </span>
  <span class="navbar-nav ms-auto" v-else>
    <span class="m-sm-1">您好，{{ this.$store.state.user.username }}{{ this.$store.getters['user/printableRole'] }}</span>
    <button type="button" class="btn btn-outline-danger mx-2" @click="$router.push('/login')">
      退出
    </button>
  </span>
</template>

<script>
import {defineComponent} from 'vue'

export default defineComponent({
  name: 'LoginButton',
  computed: {
    valid() {
      return this.$store.getters['user/valid']
    }
  }
})
</script>

<style scoped>

</style>
