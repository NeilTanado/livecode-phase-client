<template>
  <div class="container">
    <form>
      <div class="form-group">
        <label for="exampleInputEmail1">Title:</label>
        <input type="text" class="form-control"  placeholder="Enter Title" v-model="title">
      </div>
      <div class="form-group">
        <label for="exampleInputEmail1">Category:</label>
        <input type="text" class="form-control" placeholder="Enter Category" v-model="category">
      </div>
      <div class="form-group">
        <label for="exampleInputEmail1">Image:</label>
        <input type="file" class="form-control" placeholder="Insert Image" @change="fileName">
      </div>
    </form>
    <label for="exampleInputEmail1">Content:</label>
    <Vueditor ref='editor' class="mt-4"></Vueditor>
    <button class="btn btn-primary mt-3" @click="postImage()">Submit</button>
  </div>
</template>

<script>
import Vueditor from 'vueditor'
import axios from 'axios'
import swal from 'sweetalert2'

export default {
  component:{
    Vueditor
  },
  data(){
    return{
    title:'',
    category:'',
    image: null
    }
  },
  methods:{
    fileName (event) {
      this.file = event.target.files[0]
    },
    postImage: function(){
      console.log('masuk mari');
      let formData = new FormData()
      formData.append('title', this.title)
      formData.append('category', this.category)
      formData.append('content', this.$refs.editor.getContent())
      formData.append('image', this.file)
      axios.post('http://localhost:3000/articles/createarticle', formData ,{
        headers:{
          token : localStorage.getItem('token')
        }
      })
      .then((value) => {
        swal(
          'Success!',
          'You added the Item!',
          'success'
        )
      })
      .catch((err) => {
        swal(
          'Wrong!!',
          'Please Insert Some Item',
          'error'
        )
      })
    },
  }
}
</script>

<style lang="css">
</style>
