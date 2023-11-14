<template>

<h1>Register</h1>
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
  <br/>
  <button type="submit" class="btn btn-primary">Submit</button>
</form>
	
</template>

<script>
  export default {
    name: 'Register',
      data() {
      return {
      email: '',
      password: '',
    }
    },
      methods: {
        async handleSubmit (){

          const response = await fetch('auth/register', {  
          method: "post",
          headers: {
            'Accept': 'application/json',
            'Content-Type': 'application/json'
          },
          //make sure to serialize your JSON body
          body: JSON.stringify({
              email: this.email,
              password: this.password 
            })
          });

          console.log(response.json());
          await this.$router.push('/login'); 
        }
      }
    }
</script>   
