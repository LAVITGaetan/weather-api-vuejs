<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          v-model="query"
          type="text"
          placeholder="Search..."
          class="search-bar"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
          <div class="date">Monday 15 January 2000</div>
          <div class="temp">{{ Math.round(weather.main.temp) }}</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      api_key: "855515243766fe7606b3b5703cf16cf4",
      api_uri: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter") {
        fetch(
          `${this.api_uri}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
      console.log(this.weather);
    },
  },
};
</script>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: Montserrat;
}

#app {
  width: 100vw;
  height: 100vh;
  background-image: url("./assets/cold-bg.jpg");
  background-repeat: no-repeat;
  background-size: cover;
  background-position: center;
}
main {
  width: 100vw;
  min-height: 100vh;
  background: #00000010;
  padding: 15px;
}

.search-box {
  width: 80%;
  margin: auto;
}

.search-bar {
  width: 100%;
  outline: none;
  border: 2px solid #f1f3f5;
  border-radius: 50px;
  padding: 0.7em 1.4em;
}
</style>
