<template>
  <div id="app">
    <main>
     <div class="search-box">
       <input type="text" 
       class="search-bar" 
       placeholder="Search..."
        v-model="query"
        @keypress="fetchWeather">
   
     </div>
    
     <div class="weather-wrap" v-if="typeof weather.main != 'undefined' ">
       <div class="location-box">
       <div class="location">{{weather.name}},{{weather.sys.country}}</div>
         <div class="date">Monday 29 january</div>
     </div>
     <div class="weather-box">
       <div class="temp">{{Math.round(weather.main.temp)}}°C</div>
       <div class="weather">{{weather.weather[0].main}}</div>
       </div>
         </div>
       
       
    </main>
 
  </div>
</template>

<script>


export default {
  name: 'App',
  data () {
  return{
   api_key: '28998319256bdf4554a86fe420060ba2',
   url_base: 'https://cors-anywhere.herokuapp.com/http://api.openweathermap.org/data/2.5/',
   query: '',
   weather:{}
  }
 },
 methods:{
   fetchWeather  (e) {
     if(e.key == "Enter"){
      fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
      .then(res => {
        return res.json();
      }).then(this.setResults);
      }
   },
   setResults(results){
     this.weather = results;
   }
 }
}
</script>

<style>
*{
  margin:0;
  padding:0;
  box-sizing: border-box;
  }

  #app{
    background-image: url('./assets/cold-bg.jpg');
    background-size: cover;
    background-position: bottom;
    transition: 0.4s;
  }

  main{
    min-height: 100vh;
    padding:25px;
    background-image: linear-gradient(to bottom, rgba(0,0,0,0.25),rgba(0,0,0,0.75));
  }

  .search-box{
    width: 100%;
    margin-bottom: 30px;
  }

  .search-box .search-bar{
        display:block;
        width: 100%;
        padding:15px;
        color:#313131;
        font-size:20px;
        appearance: none;
        border: none;
        outline: none;
        background: none;
        box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
        background-color: rgba(255,255,255,0.5);
        border-radius:0px 16px 0px 16px;
        transition:0.4s
  }

  .search-box .search-bar:focus{
    box-shadow:0px 0px 16px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.75);
    border-radius:0px 16px 0px 16px;
  }

  .location-box .location{
    color: white;
    font-size:32px;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,0.25);
  }
  .location-box .date{
    color: white;
    font-size:20px;
    text-align: center;
    text-shadow: 1px 3px rgba(0,0,0,0.25);
  }

  .weather-box{
    text-align: center;
  }

  .weather-box .temp{
    display: inline-block;
    padding: 10px 25px;
    color: white;
    font-size:102px;
    font-weight: 900;
    text-shadow: 3px 6px rgba(0,0,0,0.25);
    background-color: rgba(255,255,255,0.25);
    border-radius: 16px;
    margin:30px 0px;
    box-shadow: 3px 6px rgba(0,0,0,0.25);
  }

  .weather-box .weather{
    color: white;
    font-size: 48px;
    font-style: italic;
    text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
    font-weight: 600;
  }



</style>


