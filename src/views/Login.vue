<template>
  <div class="login w-1/4 relative">
    <div 
      class="
      p-8
      z-10

      border-solid
      border-4
      border-gray-400

      flex
      flex-col
      justify-end
      items-center
      "
    >
        <h1
          class="
          mb-8
          uppercase
          font-bold
          text-xl
          "
        >
          Вход
        </h1>
        <div
          class="
          animate-bounce
          w-80
          mb-12
          font-bold

          flex
          justify-between
          "
        >
          <label 
            for="formEmail"
          >
            Email:
          </label>
          <input 

          type="email"
          id="formEmail"
          name="formEmail"
          v-model="loginEmail"
          class="
          p-0.5
          border-solid
          border-2
          border-black
          "
          >
        </div>
        <div
          class="
          animate-bounce
          w-80
          mb-12
          font-bold

          flex
          justify-between
          "
        >
          <label
            for="formPassword"
          >
            Пароль:
          </label>
          <input 
          type="password"
          id="formPassword"
          name="formPassword"
          v-model="loginPassword"
          class="
          p-0.5
          border-solid
          border-2
          border-black
          "
          >
        </div>
        <div
          class="
          w-80

          flex
          justify-between
          "
        >
          <button
            class="
            p-2
            uppercase

            border-dashed
            border-2
            border-black

            bg-blue-600 
            hover:bg-red-600
            text-white

            rounded-lg

            transition 
            duration-500 
            ease-in-out 
            bg-white 
            hover:bg-red-600 
            hover:text-white
            transform 
            hover:-translate-y-1 
            hover:scale-110
            "
            @click="login"
          >Вход</button>
          <button
            @click="goToRecoveryPassword"
            class="
            p-2
            uppercase

            border-dashed
            border-2
            border-black

            bg-blue-600 
            hover:bg-red-600
            text-white

            rounded-lg

            transition 
            duration-500 
            ease-in-out 
            bg-white 
            hover:bg-red-600 
            hover:text-white
            transform 
            hover:-translate-y-1 
            hover:scale-110
            "
          >Восстановить пароль</button>
        </div>
    </div>
    <div 
      class="
        login-true-validate
        absolute
        px-2
        py-8
        top-24
        left-8
        z-20
        bg-gray-50
        
        flex
        flex-col
        justify-between
        items-center
        content-between

        border-solid
        border-2
        border-black
      "
      v-show="isValidate"
    >
      <div class="login-validate-text">
        <span class="block">Вы вошли под своей учётной записью.</span>
        <span class="block">Для перехода на главную страницу - нажмите кнопку "ПЕРЕЙТИ".</span>
      </div>
      <div v-show="progressBarShow" class="dt-progress-bar-container relative max-w-xl rounded-full overflow-hidden w-full h-full">
        <div class="h-3 relative max-w-xl rounded-full overflow-hidden">
          <div class="w-full h-full bg-gray-200 absolute"></div>
          <div id="bar" class="h-full bg-green-500 relative w-0" :style="{'width' : progress + '%'}"></div>
        </div>
      </div>
      <button 
      class="
      flex
      items-center

      uppercase
      font-bold

      border-solid
      border-2
      border-black

      mt-2
      mb-2
      p-2
      "
      @click="goToHomepage"
      >
        <svg class="animate-spin -ml-1 mr-3 h-8 w-8 text-black" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24">
          <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4"></circle>
          <path class="opacity-75" fill="currentColor" d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"></path>
        </svg>
        Перейти
      </button>
    </div>
    <div 
      v-show="isNotValidate"
      class="
        absolute 
        p-4
        top-20 
        left-16
        z-20
        bg-gray-50

        border-solid
        border-2
        border-black
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
      <div 
        class="
          login-no-validate-btns
          flex
          flex-col
          justify-center
          content-center
          items-center
        "
      >
        <button 
          class="
            border-solid
            border-2
            border-black

            w-36
            p-2
            mt-1
            mb-2
          "
          @click="retryingInput"
        >
          Повторить ввод
        </button>
        <button 
          class="
            border-solid
            border-2
            border-black

            w-36
            p-2
            mb-0
          "
          @click="goToHomepage"
        >
          На главную
        </button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Login',
  data: () => ({
    progress: 0,
    invervalSpeed: 10,
    incrementSpeed: 0.5,
    progressBarShow: false,
    loginEmail: '',
    loginPassword: '',
    isValidate: false,
    isNotValidate: false
  }),
  methods: {
    //Отправка логина на сервер
    login() {
      let resultValidate = this.loginValidate(this.loginEmail)
      if(resultValidate) {
        this.isValidate = true
      } else {
        this.isNotValidate = true
      }
    },

    // Проверка логина на валидность
    loginValidate(email) {
      const pattern = /[a-z0-9!#$%&'*+/=?^_`{|}~-]+(?:\.[a-z0-9!#$%&'*+/=?^_`{|}~-]+)*@(?:[a-z0-9](?:[a-z0-9-]*[a-z0-9])?\.)+[a-z0-9](?:[a-z0-9-]*[a-z0-9])?/
      return pattern.test(String(email).toLowerCase())
    },

    // Переход на главную страницу
    goToHomepage() {
      this.progressBarShow = true
      this.progressBar()
    },

    //Переход на страницу восстановления пароля
    goToRecoveryPassword() {
      this.$router.push('/recoveryPassword')
    },

    // Повторный ввод почты
    retryingInput() {
      this.isNotValidate = false
      this.loginEmail = ''
      this.loginPassword = ''
    },

    progressBar() {
      let intval = setInterval(() => {
        if(this.progress < 100) {
          this.progress += this.incrementSpeed
        }
        else {
          clearInterval(intval)
          this.$router.push('/')
        }
      }, this.invervalSpeed)
    }
  }
}
</script>

<style>

</style>