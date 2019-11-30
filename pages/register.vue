<template>
  <div class="container">
    <div class="row justify-content-center mt-5">
      <div class="col-md-6">
          <h2>Register</h2>
          <br>
        <form @submit.prevent="submit">
          <div class="form-group">
            <label for="name">Full Name:</label>
            <input type="text" v-model.trim="form.name" class="form-control" id="name" placeholder="Enter full name" name="name">
              <small class="form-text text-danger" v-if="errors.name">{{ errors.name[0]}}</small>
          </div>
          <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" v-model.trim="form.email" class="form-control" id="email" placeholder="Enter email" name="email">
            <small class="form-text text-danger" v-if="errors.email">{{ errors.email[0]}}</small>
          </div>
          <div class="form-group">
            <label for="pwd">Password:</label>
            <input type="password" v-model.trim="form.password" class="form-control" id="pwd" placeholder="Enter password" name="pswd">
             <small class="form-text text-danger" v-if="errors.password">{{ errors.password[0]}}</small>
          </div>
          <div class="form-group form-check">
            <label class="form-check-label">
              <input class="form-check-input" type="checkbox" name="remember"> Remember me
            </label>
          </div>
          <button type="submit" class="btn btn-primary">Register</button>
        </form>
        <br>
        <p>You have an account? <nuxt-link to="/login">Login</nuxt-link></p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    name: "register",
    data(){
      return {
        form:{
          name:'',
          email:'',
          password:''
        }
      }
    },
    methods:{
      async submit(){
        await  this.$axios.$post('register',this.form);
        await  this.$auth.loginWith('local',{
          data:{
            email: this.form.email,
            password: this.form.password
          }
        });
        //redirect
        this.$router.push('')
      }
    }
  }
</script>

<style scoped>

</style>
