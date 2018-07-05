<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">BlogNgePress</a>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <router-link class="nav-link" :to="{ path: '/'}">Home</router-link>
          </li>
          <li class="nav-item">
              <router-link class="nav-link" :to="{ path: '/about'}">About</router-link>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <div v-if="isLogin">
            <button class="btn btn-outline-success my-2 my-sm-0 mr-3" @click="createArticle()">Make Article</button>
            <button class="btn btn-outline-warning my-2 my-sm-0" @click="logout()">Logout</button>
          </div>
          <div v-else>
            <button class="btn btn-outline-warning my-2 my-sm-0" @click="toLogin()">Login</button>
          </div>
        </form>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  data(){
    return{
      isLogin : false
    }
  },
  methods:{
    toLogin(){
      this.$router.push('/login')
    },
    createArticle(){
      this.$router.push('/make')
    },
    cekLogin(){
      if(localStorage.getItem('token')){
        this.isLogin = true
      }else{
        this.isLogin = false
      }
    },
    logout(){
      localStorage.clear()
      this.cekLogin()
    }
  },
  created(){
    this.cekLogin()
  }
}
</script>

<style lang="css">
</style>
