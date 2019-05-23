<template>
  <!-- <AuthWeChat> -->
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <LoginFunction
      :is_vue_component="true"
      :options="{
        phoneInputId: 'phoneInput',
        smsCodeInputId: 'smsCodeInput',
        loginButtonId: 'loginButton',
        smsCodeButtonId: 'smsCodeButton',
      }"
    >
      <LoginForm></LoginForm>
    </LoginFunction>
    <LoginFunction
      :is_vue_component="false"
      :options="{
        phoneInputId: 'phoneInput',
        smsCodeInputId: 'smsCodeInput',
        loginButtonId: 'loginButton',
        smsCodeButtonId: 'smsCodeButton',
      }"
    >
      <div class="login-form">
        <input ref="phoneInput" class="input" placeholder="输入手机号码" />
        <input ref="smsCodeInput" class="input" placeholder="输入验证码" />
        <button id="smsCodeButton">发送验证码</button>
        <button id="loginButton">登录</button>
      </div>
    </LoginFunction>
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
  <!-- </AuthWeChat> -->
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import LoginFunction from './components/LoginFunction'
// import AuthWeChat from './components/AuthWeChat'
import LoginForm from './components/LoginForm'

export default {
  name: 'app',
  components: {
    HelloWorld,
    LoginFunction,
    // AuthWeChat,
    LoginForm,
  },
  data() {
    return {}
  },
  methods: {},
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.login-form {
  padding: 100px 20px 0 20px;
  width: 80%;

  display: flex;
  flex-direction: column;
}

.input {
  border: #2c3e50 solid 1px;
  height: 30px;
}
</style>
