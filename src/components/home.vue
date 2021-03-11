<template>
    <div>
<el-button type="primary" size="default" @click="loginOut">退出登录</el-button>

    </div>
</template>
<script>
export default {
  methods: {
    loginOut () {
      window.sessionStorage.clear('token')
      this.$router.push('/login')
    }
  }
}
</script>
<style lang="less" scoped>

</style>
