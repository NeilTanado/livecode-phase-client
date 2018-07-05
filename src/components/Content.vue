<template>
  <div class="container">
    <center>
      <div class="card mt-3" style="width: 45rem;" v-for="article in articles">
        <div class="card-body">
          <button type="button" class="close float-sm-right" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
          <div class="text-left">
            <h5 class="card-title">{{article.title}}</h5>
            <h6 class="card-subtitle mb-2 text-muted">{{article.category}}</h6>
            <button class="fas fa-pen close float-sm-right" style="font-size: 15px;"></button>
          </div>
          <p class="card-text cuttext">{{article.content}} ...</p>
          <div class="float-right">
            <router-link class="card-link" :to="{ path: '/read', query: {id:article._id,title:article.title,content:article.content,image:article.image,author:article.author,category:article.category} }">Read More</router-link>
          </div>
        </div>
      </div>
    </center>
  </div>
</template>

<script>
import axios from 'axios'
export default {
  data(){
    return{
      articles : []
    }
  },
  methods:{
    getData(){
      axios.get('http://localhost:3000/articles/dataarticle')
      .then((value) => {
        console.log(value.data.data);
        this.articles = value.data.data
      })
      .catch((err) => {
        console.log(err);
      })
    }
  },
  created(){
    this.getData()
  }
}
</script>

<style lang="css">
.cuttext {
  white-space: nowrap;
  width: 400px;
  overflow: hidden;
  text-overflow: "----";
}
</style>
