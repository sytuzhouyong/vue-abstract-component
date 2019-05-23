<script>
/* eslint-disable no-console */
export default {
  name: 'login-function',
  abstract: true, // 标记为抽象组件
  props: {
    // 子组件是否是vue组件
    is_vue_component: {
      type: Boolean,
      default: false,
    },
    options: {
      type: Object,
      default() {
        return {}
      },
    },
  },
  data() {
    return {
      phone_input: null,
      sms_code_input: null,
    }
  },
  mounted() {
    console.log('mounted')
    if (this.is_vue_component) {
      this.login_function()
    }
  },
  render() {
    // 如果子组件绑定了vmodel，那么每次值发生变化就会触发render函数调用
    console.log('render()')
    let vnodes = this.$slots.default // 子组件node
    if (!this.is_vue_component) {
      this.login_function()
    }
    return vnodes[0]
  },

  methods: {
    // 绑定了v-model，值存储在vnode.data.domProps.value + vnode.elm.value
    // 没有绑定v-model，值存储在vnode.elm.value
    send_sms_code_button_handler() {
      console.log('send_sms_code_button_handler')

      var phoneNumber =
        (this.phone_input.elm && this.phone_input.elm.value) || this.phone_input.value
      console.log(phoneNumber)
    },
    login_button_handler() {
      console.log('login_button_handler')
      var smsCode =
        (this.sms_code_input.elm && this.sms_code_input.elm.value) || this.sms_code_input.value
      console.log(smsCode)
    },

    login_function() {
      let vnodes = this.$slots.default // 子组件node

      var element_dict = {}
      for (let index = 0; index < vnodes.length; index++) {
        const node = vnodes[index]
        this.find_login_element_in_node(node, element_dict)
      }

      var login_button = element_dict[this.options.loginButtonId]
      var sms_code_button = element_dict[this.options.smsCodeButtonId]
      this.phone_input = element_dict[this.options.phoneInputId]
      this.sms_code_input = element_dict[this.options.smsCodeInputId]

      // let event = get(sms_code_button, `data.on[click]`)
      this.set_event_handler_on_node(sms_code_button, 'click', this.send_sms_code_button_handler)
      this.set_event_handler_on_node(login_button, 'click', this.login_button_handler)
    },

    find_login_element_in_node(node, element_dict) {
      var tag = node.tag || node.tagName
      console.log(`<${tag}>`)
      console.log(node)
      if (this.options.length <= 0) {
        return {}
      }

      let login_input_id = this.options.phoneInputId
      let sms_input_id = this.options.smsCodeInputId
      let login_button_id = this.options.loginButtonId
      let sms_code_button_id = this.options.smsCodeButtonId
      // 是input组件，说明找到了输入框
      if (this.is_element_match_key(node, login_input_id)) {
        element_dict[login_input_id] = node
        return element_dict
      } else if (this.is_element_match_key(node, sms_input_id)) {
        element_dict[sms_input_id] = node
        return element_dict
      } else if (this.is_element_match_key(node, login_button_id)) {
        element_dict[login_button_id] = node
        return element_dict
      } else if (this.is_element_match_key(node, sms_code_button_id)) {
        element_dict[sms_code_button_id] = node
        return element_dict
      }

      let node_tag = this.tag_of_node(node)
      var children = node_tag.indexOf('vue-component') != -1 ? node.elm.childNodes : node.children
      if (children === undefined || children.length === 0) {
        return
      }

      for (let i = 0; i < children.length; i++) {
        var item = children[i]
        this.find_login_element_in_node(item, element_dict)
      }
    },
    // 设置vnode绑定的事件处理函数
    set_event_handler_on_node(node, event_name, handler) {
      if (node === undefined) {
        console.log(`set_event_handler_on_node: node is undefined`)
        return
      }
      // 不在vue组件中的标签
      if (node.data) {
        if (!node.data.on) {
          node.data.on = {}
        }
        node.data.on[event_name] = handler
      } else {
        node.onclick = handler
      }
    },
    // node是vue组件中的标签时取tagName，否则取tag
    tag_of_node(node) {
      return node.tag || node.tagName
    },
    is_element_match_key(node, key) {
      // 不在vue组件中的标签的属性
      if (node.data && node.data.ref === key) {
        return true
      }
      if (node.data && node.data.attrs && node.data.attrs['id'] === key) {
        return true
      }
      // 在vue组件中的标签的id属性
      if (node.id === key) {
        return true
      }
      return false
    },
  },
}
</script>
<style scoped></style>
