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
        <span class="block">Сейчас вы будете перемещены на главную страницу.</span>
      </div>
      <button 
      class="
      border-solid
      border-2
      border-black

      w-24

      mt-2
      mb-0
      p-2
      "
      @click="goToHomepage"
      >
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
      this.$router.push('/')
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
    }
  }
}
</script>

<style>

</style>