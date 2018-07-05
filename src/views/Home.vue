<template>
  <div>
    <Header/>
    <Content/>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from '@/components/Header.vue'
import Content from '@/components/Content.vue'

export default {
  name: 'home',
  components: {
    Header,
    Content
  }
}
</script>
