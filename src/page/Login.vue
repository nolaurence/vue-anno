<template>
  <div class="container">
      <LoginForm class="login-form" @success="onLoginSucceed" />
      <!--      <router-link v-if="resetPasswordButtonVisible" class="tip" :to="{ name: 'ResetPassword' }">-->
      <!--        找回密码-->
      <!--      </router-link>-->
      <!--      <a class="tip" @click="handleToggleShowApiForm">-->
      <!--        <a-icon type="setting" />-->
      <!--      </a>-->
  </div>
</template>

<script>
import {mapActions, mapGetters, mapMutations } from 'vuex'

import LoginForm from "@/components/LoginForm"

export default {
  components: {
    LoginForm
  },
  // data() {
  //   return {
  //     resetPasswordButtonVisible: false,
  //     apiForm: {
  //       apiUrl: window.location.host,
  //       visible: false
  //     }
  //   }
  // },
  beforeMount() {
    this.handleVerifyIsInstall()
  },
  methods: {
    ...mapActions(['refreshUserCache', 'refreshOptionsCache']),
    onLoginSucceed() {
      // Refresh the user info
      this.refreshUserCache()
      this.refreshOptionsCache()
      if (this.$route.query.redirect) {
        this.$router.replace(this.$route.query.redirect)
      } else {
        this.$router.replace({name: 'Dashboard'})
      }
    }
    // ...mapMutations({
    //   setApiUrl: 'SET_API_URL',
    //   restoreApiUrl: 'RESTORE_API_URL'
    // }),
    // onRegisterResetPasswordKeydown(e) {
    //   // Windows / Linux: Shift + Alt + h
    //   // maxOS: Shift + Command + h
    //   if (e.keyCode === 72 && (e.altKey || e.metaKey) && e.shiftKey) {
    //     e.preventDefault()
    //     this.resetPasswordButtonVisible = !this.resetPasswordButtonVisible
    //   }
    // },
    // async handleVerifyIsInstall() {
    //   const response = await adminApi.isInstalled()
    //   if (!response.data.data) {
    //     await this.$router.push({ name: 'Install' })
    //   }
    // },

    // handleModifyApiUrl() {
    //   this.setApiUrl(this.apiForm.apiUrl)
    //   this.apiForm.visible = false
    // },
    // handleRestoreApiUrl() {
    //   this.restoreApiUrl()
    //   this.apiForm.apiUrl = this.defaultApiUrl
    // },
    // handleToggleShowApiForm() {
    //   this.apiForm.visible = !this.apiForm.visible
    //   if (this.apiForm.visible) {
    //     this.apiForm.apiUrl = this.defaultApiUrl
    //   }
    // }
  }
}

</script>

<style>
.container {
  width: 100vw;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
}

.login-form {
  display: flex;
  justify-content: center;
  width: 300px;
  height: 300px;
  border-radius: 5px;
  box-shadow: 0 4px 16px 0
    rgba(0, 0, 0, 0.1);
  padding: 20px;
}
</style>
