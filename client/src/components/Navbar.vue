<script>
    import { RouterLink } from 'vue-router';
    import { useCounterStore } from '../stores/counter';
    import { mapWritableState } from 'pinia';
    import Modal from '../components/ModalComment.vue'
    export default {
        components: { Modal },
        computed: {
          ...mapWritableState(useCounterStore, ['isLogin'])
        },
        methods: {
          logout(){
            localStorage.clear()
            this.isLogin = false
            this.$router.push('/login')
          }
        }
    }
</script>

<template>
    <nav class="navbar navbar-expand-lg bg-light">
  <div class="container">
    <RouterLink to="/" class="navbar-brand" href="#">
      <img class="rounded-circle" width="50" height="50" src="https://i.pinimg.com/originals/48/5d/85/485d855aed063b71ff31ba6998fd55d2.jpg"/>
    </RouterLink>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent" aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarSupportedContent">
      <ul class="navbar-nav me-auto mb-2 mb-lg-0">
        <li class="nav-item">
          <RouterLink to="/" class="nav-link active" aria-current="page" href="#">Home</RouterLink>
        </li>
        <li class="nav-item">
          <RouterLink to="/login" v-if="!isLogin" class="nav-link" href="#">Login</RouterLink>
        </li>
        <li class="nav-item">
          <a @click.prevent="logout" v-if="isLogin" class="nav-link" href="#">Logout</a>
        </li>
        <li class="nav-item">
          <RouterLink to="/register" v-if="!isLogin" class="nav-link" href="#">Register</RouterLink>
        </li>
        <!-- <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Dropdown
          </a>
          <ul class="dropdown-menu">
            <li><a class="dropdown-item" href="#">Action</a></li>
            <li><a class="dropdown-item" href="#">Another action</a></li>
            <li><hr class="dropdown-divider"></li>
            <li><a class="dropdown-item" href="#">Something else here</a></li>
          </ul>
        </li> -->
        <li class="nav-item">
          <Modal v-if="isLogin" class="nav-link"/>
        </li>
      </ul>
      <!-- <form class="d-flex" role="search">
        <input class="form-control me-2" type="search" placeholder="Search" aria-label="Search">
        <button class="btn btn-outline-success" type="submit">Search</button>
      </form> -->
    </div>
  </div>
</nav>
</template>