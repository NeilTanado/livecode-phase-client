<template>
  <div class="container">
    <div class="card mb-3 mt-4">
      <img class="card-img-top" src="https://storage.googleapis.com/ecommerce-hacktiv/1530775144252.jpg" alt="Card image cap">
      <div class="card-body">
        <h3 class="card-title">{{title}}</h3>
        <h5 class="card-title"> category : {{category}}</h5>
        <p class="card-text">{{content}}</p>
        <p class="card-text text-muted">{{author.name}}</p>
        <router-link :to="{ path: '/' }">Back</router-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data(){
    return{
      title : '',
      image : '',
      content: '',
      category: '',
      id: '',
      author: {},
    }
  },
  created(){
    this.title = this.$route.query.title,
    this.content = this.$route.query.content,
    this.category = this.$route.query.category,
    this.id = this.$route.query.id,
    this.author = this.$route.query.author,
    this.image = this.$route.query.image
  }
}
</script>

<style lang="css">
</style>
