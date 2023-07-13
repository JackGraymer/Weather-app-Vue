<template>
    <main>
      <div class="search-box">
        <input 
        type="text" 
        class="search-bar" 
        placeholder="Search a place"
        v-model="query"
        v-on:keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name}}, {{ weather.sys.country  }} </div>
          <div class="date">{{ getDate() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }} °C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>   
          <div class="weather-description">{{ weather.weather[0].description }}</div>       
        </div>
      </div>

    </main>

</template>

<script>

export default {
  name: 'App',
  data () {
    return {
      api_key: '9bd11661b685830edd9f9e956ec5786a',
      url_base: 'https://api.openweathermap.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods:{
    fetchWeather(e){
      if(e.key == 'Enter'){
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&appid=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults)
        .then(this.setBackground);
      }
    },
    setResults(results){
      this.weather = results;
      console.log(this.weather);
    },
    getDate(){
      let d = new Date();
      let months = ["January","February","March","April","May","June","July","August","September","October","November","December"];
      let days = ["Sunday","Monday","Tuesday","Wednesday","Thursday","Friday","Saturday"];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day}, ${date} ${month} ${year}`
    },
    setBackground(){
      let t = this.weather.main.temp;
      let img = ''
      if(t < 10){
        document.querySelector('main').style.backgroundImage = "url('./images/warm.jpg')";
        img = "cold";
      }else if (t >= 10 && t < 20){
        img = "warm";
      }
      else{
        img = "hot";
      }
      document.querySelector('main').style.backgroundImage = `url('./images/${img}.jpg')`;
    }
  }
}

</script>

<style scoped>

  main{
    background-image: url('../src/assets/images/warm.jpg');
    background-position: center;
    background-size: cover;
    transition: background-image 0.5s ease-in-out;
    -webkit-transition: background-image 0.5s ease-in-out;
  }
</style>
