<template>  
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container-fluid">
      <div class="collapse navbar-collapse" id="navbarNav">
        <router-link to="/" class="nav-link active" aria-current="page" >Home</router-link>
        <ul class="navbar-nav" v-if="!user">
          <li class="nav-item">
            <router-link to="/login" class="nav-link" >Login</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/register" class="nav-link" >Sign in</router-link>
          </li>                                                   
        </ul>   

        <ul class="navbar-nav" v-if="user">
          <li class="nav-item">
            <a href="javascript:void(0)" @click="handleClick" class="nav-link" >Logout</a>
          </li>                                                  
        </ul>                 
      </div>
    </div>  
  </nav>
</template>

<script>
  import { mapGetters } from 'vuex';

    export default {
      name: 'Nav',
      methods: {
        handleClick() {
          localStorage.removeItem('token');
          this.$store.dispatch('user', null);
          this.$router.push('/'); 
        }
      },
      computed: {
      ...mapGetters(['user'])
      }
    }
</script>    