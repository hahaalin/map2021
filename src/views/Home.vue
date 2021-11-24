<template>
<i class="fas fa-align-left"></i>
  <div class="home">
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
  </div>

      <div class="flex justify-evenly p-10 focus-within:bg-green-100 group">
    <box class="bg-red-500 hover:bg-red-400 ring-red-300 focus:ring-4 group-hover:text-gray-600 font-bold flex justify-center items-center rounded-md cursor-pointer outline-none w-20 h-20 text-3xl text-white" tabindex="0">
      1
    </box>
    <box class="bg-blue-500 hover:bg-blue-400 ring-blue-300 focus:ring-4 group-hover:text-gray-600 font-bold flex justify-center items-center rounded-md cursor-pointer outline-none w-20 h-20 text-3xl text-white" tabindex="1">
      2
    </box>
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  }
}
</script>
