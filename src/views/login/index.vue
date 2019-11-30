<template>
  <div class="login">
    <!-- 导航 -->
    <!-- #3296fa -->
    <van-nav-bar title="登陆" />
    <!-- 输入框 -->
    <!-- van-cell-group 仅仅是提供了一个上下外边框，能看到包裹的区域 -->
        <van-cell-group>
        <van-field
            v-model="user.mobile"
            required
            clearable
            label="手机号"
            placeholder="请输入手机号"
        />

        <van-field
            v-model="user.code"
            type="password"
            label="验证码"
            placeholder="请输入验证码"
            required
        />
      <!-- 登陆按钮 -->
      <div class="login-btn-box">
          <van-button type="info" @click="onLogin">登陆</van-button>
      </div>
    </van-cell-group>
  </div>
</template>

<script>
import { login } from '@/api/user'

export default {
  name: 'LoginPage',
  components: {},
  props: {},
  data () {
    return {
      user: {
        mobile: '13911111111',
        code: '246810'
      }
    }
  },
  computed: {},
  watch: {
  },
  created () {},
  methods: {
    async onLogin () {
      // const loginToast = this.$toast.loading({
      this.$toast.loading({
        duration: 0,
        forbidClick: true,
        message: '登录中...'
      })

      try {
        const res = await login(this.user)
        console.log('登录成功', res)

        this.$toast.success('登录成功')
      } catch (err) {
        console.log('登录失败', err)
        this.$toast.fail('登录失败，手机号或验证码错误')
      }
    }
  }
}
</script>

<style scoped lang="less">
.login {
  .login-btn-box {
    padding: 20px;
    .van-button {
      width: 100%;
    }
  }
}
</style>
