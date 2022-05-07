<template>
  <div id="app" :class="typeof weather.main!='undefined' && (weather.weather[0].main=='Clear'? 'clear': (weather.weather[0].main=='Rain'? 'rain' : (weather.weather[0].main=='Snow'? 'snow' : 'clouds')))">
    <main>
      <div class="search-box">
        <input type="text" name="" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchweather"/>
      </div>
      <div class="weather-wrap" v-if="typeof weather.main!='undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{weather.sys.country}}</div>
          <div class="date">{{setDate()}}</div>
        </div>
      

      <div class="weather-box" >
        <div class="temp"> {{ Math.round(weather.main.temp) }}°C</div>
        <div class="weather"> {{ weather.weather[0].main }} </div>
       
      </div></div>



    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data(){
    return {
      api_key: 'a66a3894aa54b5cb43849b5630b08ed0',
      url_base: 'http://api.openweathermap.org/data/2.5/',
      query:'',
      weather:{},
    }
  },
  methods:{
    fetchweather(e){
      if(e.key=="Enter"){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
        .then(res=>{
          return res.json();
        }).then(this.setResults);
      }
    },
    setResults(results){
      this.weather=results;
    },
    setDate(){
      var currentTime =new Date();
      return currentTime.getDate() + "/" + currentTime.getMonth() + "/" + currentTime.getFullYear() ;
    },
   
  }
}
</script>

<style>
*{
  margin:0;
  padding: 0;
  box-sizing:border-box;
}
body{
  font-family:'Franklin Gothic Medium', 'Arial Narrow', Arial, sans-serif;
}
#app{
  background-image:url(./assets/clouds-bg.jpg);
  background-size: cover;
  background-position:bottom;
  transition:0.4s;
}
#app.clear{
background-image:url(./assets/clear-bg.jpg);
}
#app.clouds{
  background-image:url(./assets/clouds-bg.jpg);
}
#app.rain{
  background-image:url(./assets/rain-bg.jpg);
}
#app.snow{
  background-image:url(./assets/snow-bg.jpg);
}
main{
  min-height:100vh;
  padding:25px;
  background-image: linear-gradient(to bottom,rgba(188, 204, 159, 0.25),rgba(0,0,0,0.75))
}
.search-box{
  width: 100%;
  margin-bottom:30px;
}
.search-box .search-bar{
  display:block;
  width:100%;
  padding:15px;
  color:rgb(11, 6, 54);
  font-size:20px;
  appearance:none;
  border:none;
  outline:none;
  background:none;
  background-color:rgba(255, 255, 255, 0.55);
  border-radius:0px 16px 0px 16px;
  transition: 0.4s;
  

}
.search-box .search-bar:hover{
  background-color:rgba(229, 231, 235, 0.85);
  transition: 0.4s;
}
.search-box .search-bar:focus{
  background-color:rgba(229, 231, 235, 0.95);
  box-shadow: 0px 0px 16px rgba(0,0,0,0.25);
}
.location-box .location, .location-box .date{
  color:white;
  font-size:30px;
  font-weight:500;
  text-align:center;
  text-shadow: 1px 4px rgba(0,0,0,0.25);
}
.location-box .date{
  font-size:20px;
  font-style:italic;
  padding:5px;
}
.weather-box{
  text-align:center;

}
.weather-box .temp{
  font-size:100px;
  display:inline-block;
  padding:10px 25px;
  color:white;
  font-weight:900;
  text-shadow:2px 5px 10px rgba(83, 82, 82, 0.75);
  background-color:rgba(229, 231, 235, 0.507);
  border-radius: 16px 16px 16px 16px;
  margin:30px 0px;
  box-shadow: 3px 6px 6px rgba(0,0,0,0.25);

}
.weather-box .weather{
  color:rgb(255, 255, 255);
  font-size:40px;
  font-weight:600;
  font-style:italic;
  
}
</style>
