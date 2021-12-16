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
            {{ weatherTest }}
          </div>

          <div class="date">
            Date Test
          </div>

          <div class="weatherBox">

            <div class="temperature">
              Temp Test
            </div>

            <div class="weather">
              Weather Test
            </div>

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
      url_base: "api.openweathermap.org/data/2.5/",
      input: '',
      // something that stores the requests 
      weatherTest: []
    };
  },

  methods: {
    fetchWeather() {
      fetch(`${this.url_base}weather?q=${this.input}&appid=${this.apiKey}`)
      .then(res => {
        // res.clone().json()
        // troubleshooting
        console.log(res.json())
      })
      .then(data => { 
        this.weatherTest = data
        console.log("data: " + this.weatherTest)
        })
      .catch(err => console.log("there exists an error: " + err.message))
    }

  }
}
</script>