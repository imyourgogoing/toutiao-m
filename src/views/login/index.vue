<template>
  <div>
    <van-nav-bar title="登录" />
    <van-form @submit="onSubmit">
      <van-field
        name="手机号"
        type="number"
        v-model="user.mobile"
        maxlength="11"
        placeholder="请输入手机号"
      />
      <van-field
        name="验证码"
        v-model="user.code"
        maxlength="6"
        placeholder="请输入验证码"
      >
        <template #button>
          <van-button size="small" type="primary">发送验证码</van-button>
        </template>
      </van-field>
      <div style="margin: 16px">
        <van-button block type="info" native-type="submit"> 提交 </van-button>
      </div>
    </van-form>
  </div>
</template>

<script>
import { login } from '@/api/user.js'
export default {
  name: 'LoginPage', // 名字
  data () {
    return {
      user: {
        mobile: '',
        code: ''
      }
    }
  },
  created () { }, // 钩子
  mounted () { }, // 钩子
  methods: {
    async onSubmit () {
      const user = this.user
      try {
        const res = await login(user)
        console.log('登录成功', res)
      } catch (err) {
        if (err.response.status === 400) {
          console.log('登录失败', err)
        }
      }
    }
  }
}
</script>

<style>
</style>
