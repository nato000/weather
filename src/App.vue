<template>
  <div id="app">
    <h1>Weather</h1>
    <center>
    <div class="block1" v-if='show == true'>
      id:{{air.data.id}} <br>
      From:{{air.data.cityFrom}} <br>
      To:{{air.data.cityTo}} <br>
      fly durations:{{air.data.fly_duration}} <br>
      price:{{air.data.price}} <br>
      routes:{{air.data.routes}} <br>
     
     
      <br>
      <button class="btn" @click="show = false">roll up</button>
      <br><br>
    </div>
    </center>
    <br>
    <div else>
      <input class="btn" type="text"  v-model="city1">
      <input class="btn" type="text"  v-model="city2">
      <br><br><br>
      <input class="btn" type="text"  v-model="date1">
      <input class="btn" type="text"  v-model="date2">
      <!-- <button class="btn" @click="p">Add city</button><br> <br>

        <select name="sel" id="sel" v-model="b">
        <option disabled value="">choose</option>
        <option v-for="city in cities" :key="city">{{city}}</option> 

      </select> -->
      <br>
      <br>
      <button class="btn" @click="q">Weather</button>
    </div>
  </div>
</template>
<script>

import axios from 'axios'

export default {
  name: 'App',
  data() {
    return{
     
        city1:'',
        city2:'',
        date1:'',
        date2:'',
    
        air:[],
        show: false
    }
  },
  
  methods: {
    q:function(){
    axios.get('https://api.skypicker.com/flights?fly_from='+this.city1+'&fly_to='+this.city2+'&date_from='+this.date1+'&return_from='+this.date2+'&partner=picky')
      .then((response) => {
        console.log(response.data);
        this.air = response.data;
        this.show = true;
      })
  },
  }
}
</script>

<style>
#app {
  font-size: 110%;
  text-align: center;
  color: #000000;
  margin-top: 100px;
     } 

select{
  font-size: 120%;
  width: 6%;
}
.block1 { 
 width: 300px; 
 background: rgb(172, 172, 172);
 padding: 5px;
 border: solid 1px black; 
}

.btn{
  font-size: 120%;
  background:rgb(212, 212, 212);
}
</style>
