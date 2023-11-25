<template>
    <Header/>
    <h1 class="res_text">Update Restaurant Page</h1>
    <form class="add">
        <input type="text" placeholder="Restaurant Name" name="name" v-model="restaurant.name">
        <input type="text" placeholder="Address" v-model="restaurant.address">
        <input type="text" placeholder="Contact" v-model="restaurant.contact">
        <input type="time" placeholder="open_time" v-model="restaurant.open_time">
        <input type="time" placeholder="closed_time" v-model="restaurant.closed_time">
        <div class="res_btn">
            <button type="button" @click="updateRestaurant">Upadte Restaurant</button>
        </div>
    </form>
</template>

<script>
import Header from './Header.vue';
import axios from 'axios';
    export default {
        /* eslint-disable */
        name:'Update',
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
            async updateRestaurant(){
                const result = await axios.put("http://localhost:3000/restaurant/"+ this.$route.params.id, {
                    name:this.restaurant.name,
                    address:this.restaurant.address,
                    contact:this.restaurant.contact,
                    open_time:this.restaurant.open_time,
                    closed_time:this.restaurant.closed_time
                })
                if(result.status==200){
                    this.$router.push({name:'Home'});
                }
            }
        },
        async mounted(){
            let user = localStorage.getItem('user-info')
            if(!user){
                this.$router.push({name:'SignUp'})
            }
            const result = await axios.get("http://localhost:3000/restaurant/"+ this.$route.params.id)
            this.restaurant = result.data
        },
    }
</script>

<style scoped>

</style>