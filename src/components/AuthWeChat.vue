<script>
/* eslint-disable no-console */
export default {
  name: 'auth-wechat',
  abstract: true, // 标记为抽象组件
  props: {},
  render() {
    console.log('xxx')
    // window.location.href = 'https://www.baidu.com'
    return this.$slots.default[0]
  },
}
</script>
