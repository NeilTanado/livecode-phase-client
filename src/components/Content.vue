<template>
  <div class="container">
    <center>
      <div class="card mt-3" style="width: 45rem;" v-for="article in articles">
        <div class="card-body">
          <button  @click="deleteItem(article)" type="button" class="close float-sm-right" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
          <div class="text-left">
            <h5 class="card-title">{{article.title}}</h5>
            <h6 class="card-subtitle mb-2 text-muted">{{article.category}}</h6>
            <button class="fas fa-pen close float-sm-right" data-toggle="modal" data-target="#exampleModalLong" @click="editData(article)"></button>
            <div class="modal fade" id="exampleModalLong" tabindex="-1" role="dialog" aria-labelledby="exampleModalLongTitle" aria-hidden="true">
              <div class="modal-dialog" role="document">
                <div class="modal-content">
                  <div class="modal-header">
                    <h5 class="modal-title" id="exampleModalLongTitle">Sign Up Form</h5>
                    <button type="button" class="close" data-dismiss="modal" aria-label="Close">
                      <span aria-hidden="true">&times;</span>
                    </button>
                  </div>
                  <div class="modal-body">
                    <form>
                      <div class="form-group">
                        <label class="form-control-label">Title</label>
                        <input class="form-control" type="text" v-model="name">
                      </div>
                      <div class="form-group">
                        <label class="form-control-label">Category</label>
                        <input class="form-control" type="text" v-model="email">
                      </div>
                      <div class="form-group">
                        <Vueditor ref='editor' class="mt-4"></Vueditor>
                      </div>
                    <button type="button" class="btn btn-secondary mr-4" data-dismiss="modal">Cancel</button>
                    <button class="btn btn-primary" data-dismiss="modal" @click="fiturUpdate(article)">Sign Up</button>
                  </form>
                  </div>
                </div>
              </div>
            </div>
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
import swal from 'sweetalert2'
import Vueditor from 'vueditor'

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
    },
    editItem(){

    },
    deleteItem(article){
      let self = this
      console.log(article.author._id);
      if(localStorage.getItem('userId')===article.author._id){
        axios.delete('http://localhost:3000/articles/deletearticle/'+article._id)
        .then((value) => {
          self.getData()
          swal('Berhasil Delete Article')
        })
        .catch((err) => {
          console.log(err);
        })
      }else{
        swal('Tidak bisa delete article orang lain')
      }
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
