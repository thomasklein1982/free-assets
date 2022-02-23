<template>
  <Main/>
</template>

<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import Main from './components/Main.vue'

export default{
  data(){
    return {
      version: 4
    };
  },
  components: {
    Main
  }
}
</script>