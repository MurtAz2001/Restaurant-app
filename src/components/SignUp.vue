<template>
    <div style="text-align: center;">
        <img class="logo" src="../assets/logo.png" />
    </div>
    <h1 class="res_text">Sign Up</h1>
    <div class="resgister">
        <input type="text" placeholder="Name" v-model="name">
        <input type="email" placeholder="Email" v-model="email">
        <input type="password" placeholder="Password" v-model="password">
        <div class="res_btn">
           <button class="" @click="SignUp">Sign Up</button> 
        </div>
        <p class="res_text">
            If you have account 
            <router-link to="/login">Login</router-link>
            !
        </p>
    </div>
</template>

<script>
import axios from 'axios'
    export default {
        name:'SignUp',
        data(){
            return{
                name:'',
                email:'',
                password:''
            };
        },
        methods:{
           async SignUp(){
                let result =await axios.post("http://localhost:3000/user", {
                    email:this.email,
                    name:this.name,
                    password:this.password
                });
                if(result.status=== 201){

                    localStorage.setItem("user-info",JSON.stringify(result.data))
                    this.$router.push({name:'Home'})
                }
            }
        },
        mounted(){
            let user = localStorage.getItem('user-info')
            if(user){
                this.$router.push({name:'Home'})
            }
        },
    }
</script>

<style scoped>

</style>