<template>
  <div class="container">
    <div class="row justify-content-center mt-5">
      <div class="col-md-6">
          <h2>Login</h2>
          <br>
        <form @submit.prevent="submit">
          <div class="form-group">
            <label for="email">Email:</label>
            <input type="email" class="form-control" v-model.trim="form.email" id="email" placeholder="Enter email" name="email" autofocus>
            <small class="form-text text-danger" v-if="errors.email">{{ errors.email[0]}}</small>
          </div>
          <div class="form-group">
            <label for="pwd">Password:</label>
            <input type="password" class="form-control" v-model.trim="form.password" id="pwd" placeholder="Enter password" name="pswd">
            <small class="form-text text-danger" v-if="errors.password">{{ errors.password[0]}}</small>
          </div>
          <div class="form-group form-check">
            <label class="form-check-label">
              <input class="form-check-input" type="checkbox" name="remember"> Remember me
            </label>
          </div>
          <button type="submit" class="btn btn-primary">Login</button>
        </form>
        <br>
        <p>Dont have an account? <nuxt-link to="/register">Register</nuxt-link></p>
      </div>
    </div>
  </div>
</template>

<script>
  export default {
    data(){
      return {
        form:{
          email:'',
          password:''
        }
      }
    },
    methods:{
      async submit(){
        await this.$auth.loginWith('local',{
          data:this.form
        })
        this.$router.push('/')
      }
    }
  }
</script>

<style scoped>

</style>
