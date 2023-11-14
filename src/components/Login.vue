<template>
<h2>Login</h2>
<br/>
<p>
  <strong><em>Example data:</em></strong>
  <br/>
  <strong>email</strong>: testuser@testuser.com
  <br/>
  <strong>password</strong>: testuser
</p>  
<form @submit.prevent="handleSubmit">
  <div class="form-group">
    <label for="exampleInputEmail1">Email address:</label>
    <input type="email" v-model="email" class="form-control" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Enter email">
    <small id="emailHelp" class="form-text text-muted">We'll never share your email with anyone else.</small>
  </div>
  <div class="form-group">
    <label for="exampleInputPassword1">Password:</label>
    <input type="password" v-model="password" class="form-control" id="exampleInputPassword1" placeholder="Password">
  </div>
  <div class="errormsg">{{errormsg}}</div>
  <br/>
  <button type="submit" class="btn btn-primary">Submit</button>
</form> 
</template>

<script>
    export default {
      name: 'Login',
      data() {
        return {
        email: '',
        password: '',
        errormsg: ''
      }
    },
      methods: {
        async handleSubmit (){
          const response = await fetch('auth/login', {  
            method: "post",
            headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json',
            Authorization: 'Bearer'
          },
            //make sure to serialize your JSON body
            body: JSON.stringify({
              email: this.email,
              password: this.password 
            })
          });

          const data = await response.json();
          if(data.status == 401) {
            this.errormsg = data.message; 
          }
          else {
            this.errormsg = ''; 
          }
          // console.log(data.status);
          // console.log(data.message);

          if(data.access_token){
              localStorage.setItem('token', data.access_token);
              this.$store.dispatch('user', {
                email: this.email
              });
              this.$router.push('/');     
            }        
          }    
        }
    }
</script>   

<style scoped>
.errormsg {
  color: red;
  font-style: italic;
}
</style>