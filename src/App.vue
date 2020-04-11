<template>
  <div id="app">
    <h1>Check the Weather</h1>
     <input v-model="message" v-on:change="api" placeholder="Choose a name of the City"><button v-on:click="clear">x</button>
    <button id="select" v-on:click="Add">Select</button>
    <div class="content">
    <div class="gridElement" v-show="selected"><ChosenWeather :img="img" />Temperature in {{this.city[this.city.length - 1]}} is {{this.temperature[this.temperature.length - 1]}} C</div>
    <div class="gridElement" v-on:click="local"><h2>Click to Check the weather in your city</h2></div>
    <div class="gridElement"><p>History of previously chosen cities: </p>{{this.city[this.city.length-1]}}  {{this.city[this.city.length-2]}} {{this.city[this.city.length-3]}} {{this.city[this.city.length-4]}} {{this.city[this.city.length-5]}} {{this.city[this.city.length-6]}} {{this.city[this.city.length-7]}} {{this.city[this.city.length-8]}} {{this.city[this.city.length-9]}} {{this.city[this.city.length-10]}}</div>
    <div class="gridElement">Previous City: <p>{{this.city[this.city.length - 2]}}</p>
      <p>Temperature: {{this.temperature[this.temperature.length - 2]}}</p>
    </div>
    
   </div>
    <footer>Created by Adam Wyka in 2020</footer>
  </div>
</template>

<script>
import ChosenWeather from './components/ChosenWeather.vue'
export default {
  name: 'App',
  components: {
    ChosenWeather
  },
  
  data(){
  return {
    selected: false,
    city: [],
    message: '',
    temperature: [],
    img: 0,
    weather: "",
  }
  },
  methods:{
    clear(){
      this.message = ""
    },
        api(){
          fetch('http://api.openweathermap.org/data/2.5/weather?q='+this.message+'&appid='+/*ADD YOUR OWN API KEY FROM OPENWEATHERMAP*/+'&mode=json&units=metric')
.then(res => res.json())
.then(data =>   {this.temperature.push(data.main.temp)
                this.weather = (data.weather[0].main)})
                },
        local(){
          if (navigator.geolocation) {
  navigator.geolocation.getCurrentPosition(getPosition);
}
function getPosition(position) {
  let lng = position.coords.longitude;
  let lat = position.coords.latitude;
fetch('http://api.openweathermap.org/data/2.5/weather?lat='+lat+'&lon='+lng+'&appid='+/*ADD YOUR OWN API KEY FROM OPENWEATHERMAP*/+'&mode=json&units=metric')
.then(res => res.json())
.then(data => {
 alert(`The weather in ${data.name}:
 Temperature: ${data.main.temp} C
 Weather Conditions: ${data.weather[0].main}`)
})
}
        },
        conditional(){
          switch(this.weather) {
  case "Clear":
    this.img = 2
    break;
  case "Rain":
    this.img = 1
    break;
    case "Snow":
    this.img = 3
    break;
    case "Clouds":
    this.img = 4
    break;
  default:
    this.img = 0
}
    },
        Add(){
          this.conditional()
          this.selected = true
          this.city.push(this.message)

           }
  }
}

</script>

<style>
#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  height: 110vh;
  width: 110vw;
  font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
  border-color: darkgreen;
  border-style: double;
  background-image: url("./assets/tlo.jpg");
  background-size: cover;
  background-repeat: no-repeat;
}
::-webkit-scrollbar {
    display: none;
}
h1{
  margin-top: 3vh;
  background-color: black;
  color: gray;
  opacity: .62;
  width: 50vw;
  height: 10vh;
  margin-left: 26%;
  font-size: 4vh;
  border-radius: 22%;

}
.content{
  display: grid;
  grid-template-columns: 1fr 1fr;
  grid-template-rows: 1fr 1fr;
}
button{
  border-radius: 50%;
  opacity: .66;
  cursor: pointer;
  margin-left: 2vw;
}
#select {
  background-color: black;
  cursor:pointer;
  padding: 14px;
  border-radius: 50%;
  font-size: 13px;
  color:green;
  margin-left: 30px;
  opacity: .6;
  font-weight: bolder;
}
#select:hover{
    opacity: .77;
    border-width: 2px;
    border-style:double;
}
h1 {
  color: blue;
}
.gridElement{
  margin-top: 8vh;
  overflow: scroll;
  color: black;
  font-size: large;
  background: rgb(34,193,195);
background: radial-gradient(circle, rgba(34,193,195,1) 0%, rgba(71,218,47,0.9248074229691877) 94%);
  opacity: .65;
  border-radius: 10%;
  font-weight: bold;
  border-color:saddlebrown;
  border-width: medium;
  border-style: solid;
  font-style: italic;
  animation-duration: 4s;
  animation-name: show;
  margin-left: 2vw;
  margin-right: 2vw;
  height: 28vh;
  width: 45vw;
  animation-duration: 5s;
  animation-name: show;
}
@keyframes show{
  from{opacity:0}
  to{opacity:65}
}
.gridElement:hover{
  opacity: .85;
}
input{
  margin-top: 5vh;
  font-size: xx-large;
  font-style: italic;
  height: 4vh;
  width: 45vw;
  background: none;
  border: none;
  border-bottom: solid;
  border-width: .4vh;
  color:goldenrod;
  text-align: center;
}
input:hover{
  border-bottom: solid;
  border-width: thick;
}
::placeholder {
  color: black;
}
:-ms-input-placeholder {
  color: black;
}
::-ms-input-placeholder { 
  color: black;
}
footer{
  font-style: italic;
  font-size: larger;
  color: royalblue;
  margin-top: 5vh;
  font-weight: bold;
}
.gridElement h2{
  margin-top: 8vh;
  text-align: center;
  cursor: pointer;
}
</style>