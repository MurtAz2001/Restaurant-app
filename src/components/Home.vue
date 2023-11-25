<template>
  <Header />
  <h1 class="res_text">Restaurant List</h1>
  
    <!-- <div class="card" v-for="item in restaurants" :key="item.id">
    <div class="card-body">
      <div class="card-text">
        <h2>{{ item.name }}</h2>
        <p>Description: {{ item.description }}</p>
        <p>Address: {{ item.address }}</p>
        <p>Contact: {{ item.contact }}</p>
        <p>open time: {{ item.open_time }}</p>
        <p>closed time: {{ item.closed_time }}</p>
        <p>menu item: {{ item.menu_items }}</p>
        <p>Total Employee: {{ item.employee_count }}</p>
        <router-link :to="'/update/' + item.id"><img class="action_logo" src="../assets/update.png" alt=""></router-link>
        <img class="action_logo" @click="deleteRestaurant(item.id)" src="../assets/delete.png" alt="">
    </div>
    </div>
  </div> -->
    <div class="list">
      <div className="card"  v-for="item in restaurants" :key="item.id"  >
        <h2 class="res_text">{{ item.name }}</h2>
        <p class="res_desc">{{ item.description }}</p>
            <div className="card-info">
                <p>{{ item.address }}</p>
                <p>{{ item.contact }}</p>
                <p>open: {{ item.open_time }}</p>
                <p>closed: {{ item.closed_time }}</p>
                <p>{{ item.menu_items }}</p>
                <router-link :to="'/update/' + item.id"><img class="action_logo" src="../assets/update.png" alt=""></router-link>
                <img class="action_logo" @click="deleteRestaurant(item.id)" src="../assets/delete.png" alt="">
            </div>
      </div>
    </div>
</template>

<script>
import Header from "./Header.vue";
import axios from "axios";
export default {
  /* eslint-disable */
  name: "Home",
  data() {
    return {
      restaurants: [],
    };
  },
  components: {
    Header,
  },
  methods: {
    async deleteRestaurant(id) {
      let result = await axios.delete("http://localhost:3000/restaurant/" + id);
      if (result.status === 200) {
        this.loadData();
      }
    },
    async loadData() {
      let user = localStorage.getItem("user-info");
      if (!user) {
        this.$router.push({ name: "SignUp" });
      }
      let result = await axios.get("http://localhost:3000/restaurant");
      this.restaurants = result.data;
    },
  },
  mounted() {
    this.loadData();
  },
};
</script>

<style scoped>
.action_logo {
  width: 20px;
  padding: 10px;
  cursor: pointer;
}

.list{
     display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr 1fr;
  gap: 2px 2px;
  grid-auto-flow: row;
}
.card {
            width: 300px;
            height: 250px;
            border-radius: 20px;
            background-color: #f3a683;
            box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
            justify-content: center;
            align-items: center;
            margin: 50px auto;
            position: relative;
            transition: 0.3s;
        }

.card:hover {
    transform: scale(1.05);
    box-shadow: 0 20px 40px rgba(0, 0, 0, 0.2);
    height: 400px;
}

.card:hover::before {
            content: "";
            position:absolute;
            width: 100%;
            height: 100%;
            border-radius: 20px;
            background: linear-gradient(45deg, #f7f7f7, #ffffff);
            mix-blend-mode: screen;
            opacity: 0.5;
            pointer-events: none;
}

        /* .card img {
            width: 100%;
            height: 100%;
            object-fit: cover;
            border-radius: 20px;
        } */

.card-info {
            display: none;
            position: absolute;
            bottom: 0;
            left: 0;
            width: 100%;
            /* background-color: rgba(255, 255, 255, 0.8); */
            background-color: #f19066  ;
            padding: 10px;
            box-sizing: border-box;
            text-align: center;
            border-radius: 20px;
}

.card:hover .card-info {
            display: block;
}
.res_desc{
  padding-left: 10px;
  text-justify:distribute-all-lines;
}
/* td{
    width: 200px;
    height: 40px;
} */
</style>