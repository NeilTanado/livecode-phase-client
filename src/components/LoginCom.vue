<template>
  <div>
      <h1 class="text-center mt-5">Stuck Overflow™</h1>
      <div class="container pt-3">
        <div class="row justify-content-sm-center">
          <div class="col-sm-10 col-md-6">
            <div class="card border-info">
              <div class="card-header">Sign in to continue</div>
              <div class="card-body">
                <div class="row">
                  <div class="col-md-4 text-center">
                    <img src="https://placeimg.com/128/128/tech/sepia" class="mb-2">
                  </div>
                  <div class="col-md-8">
                    <form class="form-signin">
                      <input type="text" class="form-control mb-2" placeholder="Email" v-model="email">
                      <input type="password" class="form-control mb-2" placeholder="Password" v-model="password">
                      <button class="btn btn-lg btn-primary btn-block mb-1" @click="fiturLogin()">Sign in</button>
                      <label class="checkbox float-left">
                    <input type="checkbox" value="remember-me">
                    Remember me
                  </label>
                    </form>
                  </div>
                </div>
              </div>
            </div>
            <a class="float-right" data-toggle="modal" data-target="#exampleModalLong">Create an account </a>

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
                        <label class="form-control-label">Name</label>
                        <input class="form-control" type="text" v-model="name">
                      </div>
                      <div class="form-group">
                        <label class="form-control-label">Email</label>
                        <input class="form-control" type="email" v-model="email">
                      </div>
                      <div class="form-group">
                        <label class="form-control-label" for="password">Password</label>
                        <input class="form-control" type="password" v-model="password">
                      </div>
                    <button type="button" class="btn btn-secondary mr-4" data-dismiss="modal">Cancel</button>
                    <button class="btn btn-primary" data-dismiss="modal" @click="fiturRegister()">Sign Up</button>
                  </form>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>
      </div>
  </div>
</template>

<script>
  import axios from 'axios'
  import swal from 'sweetalert2'

  export default {
    data(){
      return{
        email:'',
        password:'',
        name:'',
      }
    },
    methods:{
      fiturLogin: function(){
        let userLogin = {
          email : this.email,
          password : this.password
        }
        axios.post('http://localhost:3000/users/login',userLogin)
        .then((userToken) => {
          swal("Nice", "You already logged in!", "success");
          localStorage.setItem('token',userToken.data.token)
          localStorage.setItem('userId',userToken.data.id)
          this.$router.push('/')
        })
        .catch((err) => {
          console.log(err);
        })
      },
      fiturRegister: function(){
        let userRegister = {
          name: this.name,
          email : this.email,
          password : this.password
        }
        axios.post('http://localhost:3000/users/createuser',userRegister)
        .then((value) => {
          swal("Nice", "You already registered!", "success");
          this.email = ''
          this.name = ''
          this.password = ''
        })
        .catch((err) => {
          console.log(err);
        })
      },
    }
  }
</script>

<style>
</style>
