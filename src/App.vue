<template>
  <div id="app" class="container-fluid">
    <Nav />
    <h1>Simple authentication example</h1>

    <div class="auth-wrapper row">
      <div class="auth-inner col-md-6">
        <router-view />
      </div>        
    </div>  

  </div>  
</template>

<script>
    import Nav from './components/Nav.vue'
    import { mapGetters } from 'vuex';

    export default {
      name: 'App',
      computed: {
      ...mapGetters(['user'])
      },

      async created() {
        console.log(localStorage.getItem('token'));
        if (localStorage.getItem('token')){
          // since we don't have route to get user, we get it from vuex      
          this.$store.dispatch('user', {
            email: this.user.email
          });
        }
      },
        
      components: {
        Nav,
      }
    }
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
}
</style>
