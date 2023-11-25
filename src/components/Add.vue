<template>
    <Header/>
    <h1 class="res_text">Add Restaurant Page</h1>
    <form class="add">
        <input type="text" placeholder="Restaurant Name" name="name" v-model="restaurant.name">
        <input type="text" placeholder="Address" v-model="restaurant.address">
        <input type="text" placeholder="Contact" v-model="restaurant.contact">
        <input type="time" placeholder="open_time" v-model="restaurant.open_time">
        <input type="time" placeholder="closed_time" v-model="restaurant.closed_time">
        <div class="res_btn">
            <button type="button" @click="addRestaurant">Upadte Restaurant</button>
        </div>
        
    </form>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';
    export default {
        /* eslint-disable */
        name:'Add',
        components:{
            Header,
        },
        data(){
            return{
                restaurant:{
                    name:'',
                    address:'',
                    contact:'',
                    open_time:'',
                    closed_time:'',
                }
            };
        },
        methods:{
            async addRestaurant(){
                const result = await axios.post("http://localhost:3000/restaurant", {
                    name:this.restaurant.name,
                    address:this.restaurant.address,
                    contact:this.restaurant.contact,
                    open_time:this.restaurant.open_time,
                    closed_time:this.restaurant.closed_time
                })
                if(result.status==201){
                    this.$router.push({name:'Home'});
                }
            }
        },
        mounted(){
            let user = localStorage.getItem('user-info')
            if(!user){
                this.$router.push({name:'SignUp'})
            }
        },
    }
</script>

<style scoped>

</style>