<template>
  <div style="text-align: center;">
    <img class="logo" src="../assets/logo.png" />
  </div>
  <h1 class="res_text">Login</h1>
  <div class="login">
    <input type="email" placeholder="Email" v-model="email" />
    <input type="password" placeholder="Password" v-model="password" />
    <div class="res_btn">
      <button class="" @click="login">Login</button>
    </div>
    
    <p class="res_text">
      <router-link to="/sign-up">Sign Up</router-link>
    </p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  /* eslint-disable */
    name: "Login",
    data() {
      return {
        email: "",
        password: "",
      };
    },
    methods: {
      async login() {
        let result = await axios.get(
          `http://localhost:3000/user?email=${this.email}&password=${this.password}`
        );
        if (result.status === 200 & result.data.length > 0) {
          localStorage.setItem("user-info", JSON.stringify(result.data[0]));
          this.$router.push({ name: "Home" });
        }
      },
    },
    mounted(){
        let user = localStorage.getItem('user-info')
        if(user){
            this.$router.push({name:'Home'})
        }
    },
};
</script>

<style scoped>


</style>