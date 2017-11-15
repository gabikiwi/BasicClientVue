<template>
  <div class="register">
    <h1>Register</h1>
    <input type="email" name="email" v-model="email" placeholder="email"></input>
    <input type="password" v-model="password" name="password" placeholder="password"></input>
    <br>
    <div class="error" v-html="error" />
    <button @click="register">Register</button>
  </div>
</template>

<script>
  import AuthenticationService from '@/services/AuthenticationService'
  export default {
    data () {
      return {
        email: 'a',
        password: 'a',
        error: null
      }
    },
    watch: {
      email (value) {
        console.log('email has changed', value)
      }
    },
    methods: {
      async register () {
        try {
          const response = await AuthenticationService.register({
            email: this.email,
            password: this.password
          })
          console.log(response.data)
        } catch (error) {
          this.error = error.response.data.error
        }
      },
      registerTest () {
        console.log('register button was clicked', this.email, this.password)
      }
    },
    mounted () {
      setTimeout(() => {
        this.email = 'hello world'
      }, 3000)
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .error {
    color:red;
  }
</style>
