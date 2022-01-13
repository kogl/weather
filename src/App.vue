<template>
  <div
    id="app"
    :class="
      typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''
    "
  >
    <!-- <Weather /> -->
    <main>
      <div class="search-box">
        <input
          type="text"
          name=""
          id=""
          class="search-bar"
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>

          <div class="date">{{ getMeTheDate() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
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
      api_key: "5fda19c90ba93f9268dfe1cd4e91ed70",
      url: "https://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
    };
  },

  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
      }
    },
    setResults(results) {
      this.weather = results;
    },
    getMeTheDate() {
      let d = new Date();
      let months = [
        "January",
        "February",
        "March",
        "April",
        "May",
        "June",
        "July",
        "August",
        "September",
        "October",
        "November",
        "December",
      ];
      let days = [
        "Sunday",
        "Monday",
        "Tuesday",
        "Wednesday",
        "Thursday",
        "Friday",
        "Saturday",
      ];
      let day = days[d.getDay()];
      let date = d.getDate();
      let month = months[d.getMonth()];
      let year = d.getFullYear();
      return `${day} ${date} ${month} ${year}`;
    },
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=ABeeZee");
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

body {
  font-family: "ABeeZee", sans-serif;
  color: #f3f3f3;
}

#app {
  background: purple;
}

#app.warm {
  background: red;
}

main {
  height: 100vh;
  padding: 25px;
  background: linear-gradient(
    to right top,
    #d16ba575,
    #c777b975,
    #ba83ca75,
    #aa8fd875,
    #9a9ae175,
    #8aa7ec75,
    #79b3f475,
    #69bff875,
    #52cffe75,
    #41dfff75,
    #46eefa75,
    #5ffbf175
  );
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
}

.search-box .search-bar {
  display: block;
  padding: 15px;
  width: 100%;
  color: #313131;
  font-size: 23px;
  appearance: none;
  border: 0px;
  background: #ffffff50;
  outline: none;
  box-shadow: 0px 0px 10px #00000075;
  border-radius: 0px 25px 0 25px;
  transition: 0.6s;
}

.search-box .search-bar:focus {
  background: #ffffff75;
  box-shadow: 0px 0px 15px #00000075;
  border-radius: 25px 0 25px 0;
}

.location-bar .location-box {
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px #00000025;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .date {
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  text-shadow: 1px 3px #00000025;
  background: #ffffff50;
  border-radius: 12.5px;
  margin: 30px 0px;
}

.weather-box .weather {
  color: white;
  font-weight: 700;
  font-style: italic;
  text-shadow: 1px 3px #00000025;
}
</style>
