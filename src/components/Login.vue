<template>
    <div class="login-container">
<div class="login-box">
    <!-- 头像 -->
    <div class="headimg">
        <img src="../assets/logo.png" alt="">
    </div>
    <!-- 登录表单 -->
<el-form :model="loginForm"  class="login-form" :rules="loginFormRules" ref="loginFormRef">
    <!-- username -->
  <el-form-item prop="username">
    <el-input v-model="loginForm.username" prefix-icon="el-icon-user-solid"></el-input>
  </el-form-item >
  <!-- password -->
  <el-form-item prop="password">
    <el-input v-model="loginForm.password" type="password" prefix-icon="el-icon-lock"></el-input>
  </el-form-item>
  <!-- 按钮区 -->
  <el-form-item class="btns">
      <el-button type="primary" @click="login" >登录</el-button>
      <el-button type="info" @click="reset" >重置</el-button>
  </el-form-item>
</el-form>
</div>
    </div>
</template>
<script>
export default {
  data () {
    return {
      loginForm: {
        username: '',
        password: ''
      },

      loginFormRules: {
        username: [
          { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' },
          { required: true, message: '请输入用户名', trigger: 'blur' }],
        password: [{ required: true, message: '请输入密码', trigger: 'blur' }]
      }

    }
  },
  methods: {
    reset () {
      console.log(this)
      this.$refs.loginFormRef.resetFields()
    },
    login () {
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) return this.$message.erroe('参数错误!')
        const { data: res } = await this.$http.post('login', this.loginForm)
        if (res.meta.status !== 200) return this.$message.error(res.meta.msg)
        this.$message.success('登录成功!')
        window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/')
      })
    }
  }
}
</script>
<style lang="less" scoped>
.login-container{
    background-color: aqua;
    height: 100vh;
    display: flex;
    justify-content: center;
    align-items: center;
}
.login-box{
    width: 450px;
    height: 300px;
    background-color: white;
    position: relative;
    .headimg{
        position: absolute;
        left: 50%;
        transform: translate(-50%,-50%);
        height: 130px;
        width: 130px;
        border: eee solid 2px;
        border-radius: 50%;
        background-color: #eee;
        img{
       width: 100%;
       height: 100%;
       border-radius: 50%;
   }
    }
}
.login-form{
    position: absolute;
    bottom: 0;
    width: 100%;
    padding: 0 20px;
    box-sizing: border-box;
}
.btns{
    display: flex;
    justify-content: flex-end;
}
</style>
