<template>
  <div class="login-form">
    <input id="phoneInput" ref="phoneInput" class="input" placeholder="输入手机号码" />
    <input id="smsCodeInput" ref="smsCodeInput" class="input" placeholder="输入验证码" />
    <button id="smsCodeButton">
      发送验证码
    </button>
    <button id="loginButton">
      登录
    </button>
  </div>
</template>
<script>
export default {}
</script>
<style scoped>
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
