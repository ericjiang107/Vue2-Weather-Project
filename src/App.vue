<style>
  @import './assets/weather.css';
</style>

<template>
  <div id="app">
    <div class="searchBox" id="main">
      <!-- v-model takes the info stored in data and binds those two together -->
      <!-- keypress is pinned to a method in the methods section -->
      <input class="searchBar" type="text" placeholder="Enter Name" v-model="input" 
      @keydown.enter="fetchWeather" />
      <!-- v-for="example in weatherTest" -->
      <!-- test to showcase what input is below -->
      <!-- {{ input }} -->

      <div class="weatherWrapper"> 

        <div class="locationBox">
          
          <div class="location" >
            {{ weatherTest.name }}
          </div>

          <div class="date">
            Date Test
          </div>

          <div class="weatherBox">

            <!-- test to get 1 iteration of json data -->
            <div v-for="(iterate, index) in weatherTest" :key="index">
              {{index}}
            </div>

            <!-- to get the second data from within the first iteration -->
            <!-- <div v-for="(secondIterate, test) in weatherTest" :key="test">
              <div v-for="(item, key) in secondIterate" :key="key">
                {{key}}: {{item}}
              </div>
            </div> -->

            <!-- <div class="temperature" v-for="(WeatherTest, index) in WeatherTest" :key="WeatherTest.main"> 
              {{ index }} {{ WeatherTest.feels_like }}
              {{ weatherTest.main }}
            </div>

            <div class="weather" v-for="weatherInfo in WeatherTest" :key="weatherInfo.weather">  
              {{ weatherTest.main }}
            </div> -->

          </div>
        </div>
      </div>

    </div>
  </div>
</template>

<script>
export default {
  name: 'App',

  // data setting:
  data() {
    return {
      // setting in api key:
      apiKey: '2efa223f9ef044586ce8f83ccca64d0b',
      // when making requests, this is what you need to include in order to make it 
      url_base: "https://api.openweathermap.org/data/2.5/",
      input: '',
      // something that stores the requests 
      weatherTest: []
    };
  },

  methods: {
    fetchWeather() {
      fetch(`${this.url_base}weather?q=${this.input}&units=imperal&appid=${this.apiKey}`) 
      .then(res => {
        // res.clone().json()
        // troubleshooting
        console.log(res)
        return res.json();
      }).then(data => {
        this.weatherTest = data
        console.log("data: " + data)
        })
      .catch(err => console.log("there exists an error: " + err.message))
    }

  }
}
</script>