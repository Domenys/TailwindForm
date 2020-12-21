<template>
  <div id="app" class="flex flex-col justify-center items-center">
    <div id="nav" class="mb-12 flex">
      <router-link 
      to="/" 
      class="
      m-0 
      p-1 
      w-48

      text-white
      font-bold 

      border-solid 
      border-2 
      border-gray-400 
      border-r-0

      rounded-tl-lg
      rounded-bl-lg

      transition 
      duration-500 
      ease-in-out 
      bg-blue-600 
      hover:bg-red-600 
      transform 
      hover:-translate-y-1 
      hover:scale-110
      "
      >
        Главная
      </router-link>
      <router-link 
      to="/about" 
      class="
      m-0 
      p-1 
      w-48

      text-white      
      font-bold 

      border-solid 
      border-2 
      border-gray-400 
      border-r-0

      transition 
      duration-500 
      ease-in-out 
      bg-blue-600 
      hover:bg-red-600 
      transform 
      hover:-translate-y-1 
      hover:scale-110
      "
      >
        О нас
      </router-link>
      <router-link 
      to="/login" 
      class="
      m-0 
      p-1 
      w-48
      
      text-white
      font-bold 

      border-solid 
      border-2 
      border-gray-400

      rounded-tr-lg
      rounded-br-lg

      transition 
      duration-500 
      ease-in-out 
      bg-blue-600 
      hover:bg-red-600 
      transform 
      hover:-translate-y-1 
      hover:scale-110
      "
      >
        Войти
      </router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="stylus">
#app
  font-family Avenir, Helvetica, Arial, sans-serif
  -webkit-font-smoothing antialiased
  -moz-osx-font-smoothing grayscale
  text-align center
  color #2c3e50
  margin-top 60px
</style>
