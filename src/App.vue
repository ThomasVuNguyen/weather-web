<template>
<div id ="app">
  <main>
    <div class ="search-box">
      <input type ="text" class ="search-bar" placeholder="search..." v-model ="query" v-on:keypress="fetchWeather"/>
    </div>
    
    <div class ="weather-wrap" v-if="typeof weather.main!= 'undefined'">
      <div class= "location-box">
        <div class ="location">
          {{weather.name}},{{weather.sys.country}}
        </div>
        <div class= "date">
          Monday, 20, January 2020
        </div>
        <div class ="weather-box">
          <div class ="temp">
          57* C
          </div>
          <div class ="weather">
            Rain
          </div>
        </div>
      </div>
    </div>
  </main>
  </div>
</template>

<script>
export default{
  name: 'app',
  data(){
    return {
      api_key:'bbee3ef202b425d54a0f28001bba0a8b',
      url_base: 'https://api.openweathermap.org/2.5/',
      query:'',
      weather: {},

    }
  },
  methods:{
    fetchWeather(e){
      if (e.key== "Enter"){
        fetch('${this.url_base}weather?q=${this.query}@units=metric&APPID=${this.api_key}')
        .then(res =>{
          return res.json();
        } ).then(this.setResults);
      }
    },
    setResults(results){
      this.weather = results;
    }

  },
}
</script>

<style>
*{
  margin: 0px;
  padding: 0px;
  box-sizing: border-box;
}
body{
  font-family: 'monserrat', sans-serif;
}
#app{
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;

}
main{
  min-height: 100vh;
  padding: 25px;
  background-image:linear-gradient(to bottom, rgba(0,0,0,0.25), rgba(0,0,0,0.75));
}
.search-box .search-bar{
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  background: none;
  outline: none;
  background-color: rgba(255,255,255,0.5);
  border-radius: 0px 16px 0px 16px;
  box-shadow: 0px 0px 8px rgba(0,0,0,0.25);
  transition: 0.4s;

}
.search-box .search-bar:focus {
  background-color: rgba(255,255,255,0.75);
  box-shadow: 0px 0px 16px rgba(255,255,255,0.75);
  border-radius: 16px 0px 16px 0px;

}
.location-box .location{
  color: white;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0,0,0,0.25);
}
.location-box .date{
  color: white;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
  
}
.weather-box{
  text-align: center;

}
.weather-box .temp{
  display: inline-block;
  padding: 10px 25px;
  color: white;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0,0,0,0.25);
  background-color: rgba(255,255,255,0.5);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0,255,255,0.25);
}
.weather-box .weather{
  font-size: 48px;
  color: #ffffff;
  font-weight: 100px;
  font-style: italic;
  text-shadow: 3px 6px rgba(0,0,0.25);

}
</style>
