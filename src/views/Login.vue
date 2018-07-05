<template>
  <div>
    <Header/>
    <LoginCom/>
  </div>
</template>

<script>
import Header from '@/components/Header.vue'
import LoginCom from '@/components/LoginCom.vue'

export default {
  components: {
    Header,
    LoginCom,
  }
}
</script>

<style scoped>
  .footer{
    position: absolute;
    bottom: 0;
    background-color: #e3f2fd;
  }
</style>
