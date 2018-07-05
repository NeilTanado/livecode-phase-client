<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <a class="navbar-brand" href="#">BlogNgePress</a>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <li class="nav-item active">
            <a class="nav-link" href="#">Home</a>
          </li>
          <li class="nav-item">
            <a class="nav-link" href="#">About</a>
          </li>
        </ul>
        <form class="form-inline my-2 my-lg-0">
          <input class="form-control mr-sm-2" type="search" placeholder="Search" aria-label="Search">
          <button class="btn btn-outline-info my-2 my-sm-0 mr-5" type="submit">Search</button>
          <button class="btn btn-outline-warning my-2 my-sm-0" @click="toLogin()">Login</button>
        </form>
      </div>
    </nav>
  </div>
</template>

<script>
export default {
  methods:{
    toLogin(){
      this.$router.push('/login')
    }
  }
}
</script>

<style lang="css">
</style>
