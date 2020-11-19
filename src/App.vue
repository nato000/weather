<template>
  <div id="app">
    <h1>Weather</h1>
    <center>
    <div class="block1" v-if='show == true'>
      Coordinates:{{pog.coord}} <br>
      Temperature:{{pog.main.temp}} <br>
      Pressure:{{pog.main.pressure}} <br>
      Humidity:{{pog.main.humidity}} <br>
      Wind speed:{{pog.wind.speed}} <br>
      <br>
      <button class="btn" @click="show = false">roll up</button>
      <br><br>
    </div>
    </center>
    <br>
    <div else>
      <input class="btn" type="text "  v-model="a">
      <button class="btn" @click="p">Add city</button><br>
      <br><select name="sel" id="sel" v-model="b">
        <option disabled value="">choose</option>
        <option v-for="city in cities" :key="city">{{city}}</option>
      </select>
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
        a:'',
        cities:[],
        b:'',
        pog:[],
        show: false
    }
  },
  
  methods: {
    p: function(){
      this.cities.push(this.a);
    },
    q:function(){
    axios.post('https://api.openweathermap.org/data/2.5/weather?q='+this.b+'&appid=b8d67052dc6c85fb12d75983c11d464b&units=metric')
      .then((response) => {
        console.log(response.data);
        this.pog = response.data;
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
