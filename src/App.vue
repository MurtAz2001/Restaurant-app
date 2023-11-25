<template>
  <router-view/>
</template>

<script>

export default {
  name: 'App',
  
}
</script>

<style>
:root{
  background-color: #f7d794 ;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  background-color: #f7d794 ;
}
body{
padding: 0;
margin: 0;
}
.res_btn{
  text-align: center;
}
.res_text{
text-align: center;
}
.logo{
    width: 100px;
}
.resgister input , .login input, .add input{
    width: 300px;
    height: 40px;
    padding-left: 20px;
    display: block;
    margin-bottom: 30px;
    margin-left:auto;
    margin-right: auto;
    border: 1px solid skyblue;
}
.resgister button, .login button, .add button{
    width: 320px;
    height: 40px;
    border: 1px solid skyblue;
    color: white;
    background-color: skyblue;
    cursor: pointer;
}
</style>
