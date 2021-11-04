<template>
  <div class="container-wrapper animated fadeIn">
    <div class="logo">
      <embed src="../assets/logo.svg" type="image/svg+xml"/>
    </div>
    <div class="login-form">
      <LoginForm @success="onLoginSucceed" />
<!--      <router-link v-if="resetPasswordButtonVisible" class="tip" :to="{ name: 'ResetPassword' }">-->
<!--        找回密码-->
<!--      </router-link>-->
<!--      <a class="tip" @click="handleToggleShowApiForm">-->
<!--        <a-icon type="setting" />-->
<!--      </a>-->
    </div>
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
