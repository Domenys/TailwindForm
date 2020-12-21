<template>
  <div class="recovery-password relative w-1/5">
    <div 
      v-show="isRecoveryPassword"
      class="
        p-8

        border-solid
        border-4
        border-gray-400
      "
    >
      <div
        class="
          flex
          flex-col
          justify-between
          content-between
          items-between
        "
      >
        <label for="recoveryLoginEmail">Введите действующий email:</label>
        <input 
          type="email" 
          name="recoveryLoginEmail" 
          id="recoveryLoginEmail"
          v-model="loginEmail"
          class="
            p-0.5
            border-solid
            border-2
            border-black
          "
        >
        <button
          @click="recoveryEmail"
          class="
            border-solid
            border-2
            border-black

            p-2
            mt-2
            mb-2
          "
        >
          Восстановить пароль
        </button>
      </div>
    </div>
    <div 
      v-show="isRecoveryTrue"
      class="
        recovery-password-true

        flex
        flex-col
        justify-center
        content-center
        items-center
      "
    >
      <span>Проверьте почту.</span>
      <span>Там вас будет ждать инструкция по восстановлению пароля.</span>
      <button
        @click="goToHomepage"
        class="
          border-solid
          border-2
          border-black

          w-36
          p-2
          mt-2
          mb-0
        "
      >
        На главную
      </button>
    </div>
    <div
      v-show="isRecoveryFalse"
      class="
        recovery-password-false 
        absolute 

        w-98
        p-4
        inset-0
        z-20
        bg-gray-50

        border-solid
        border-2
        border-black

        flex
        flex-col
        justify-center
        content-center
        items-center
      "
    >
      <div 
        class="
          login-no-validate-text

          flex
          flex-col
          justify-center
          content-center
        "
      >
        <span>Что-то пошло не так.</span>
        <span>Проверьте правильность введённой почты!</span>
      </div>
      <button 
        @click="retryingEmail"
        class="
          border-solid
          border-2
          border-black

          p-2
          mt-2
        "
      >
        Хорошо
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecoveryPassword",
  data: () => ({
    loginEmail: '',
    isRecoveryPassword: true,
    isRecoveryTrue: false,
    isRecoveryFalse: false
  }),
  methods: {
    recoveryEmail() {
      console.log('test')
      let resultValidate = this.loginValidate(this.loginEmail)
      if(resultValidate) {
        this.isRecoveryPassword = false
        this.isRecoveryTrue = true
      } else {
        this.isRecoveryFalse = true
      }
    },

    // Проверка логина на валидность
    loginValidate(email) {
      const pattern = /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/
      return pattern.test(String(email).toLowerCase())
    },

    //Переход к повторному вводу пароля
    retryingEmail() {
      this.isRecoveryFalse = false
    },

    //Переход на главную
    goToHomepage() {
      this.$router.push('/')
    }
  }
}
</script>

<style>

</style>