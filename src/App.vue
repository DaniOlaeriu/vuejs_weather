<template>
  <div id="app">
    <div class="container">
      <div class="weather">
        <a href="#" class="weather-logo">weather.me</a>
        <div class="weather-title"></div>
        <div class="search-box">
          <input
            placeholder="Search city..."
            type="text"
            v-model="q"
            @keypress="getWeather"
          />
          <a href=""><i class="fas fa-search"></i></a>
        </div>
        <div v-if="typeof weather.main != 'undefined'" class="weather-wrap">
          <p class="temp">{{ Math.round(weather.main.temp) }}°c</p>
          <p class="location">{{ weather.name }}, {{ weather.sys.country }}</p>
          <div class="weather-details">
            <div class="date">{{ dateBuilder() }}</div>
            <div class="weather-type">{{ weather.weather[0].main }}</div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import axios from "axios";

  export default {
    name: "App",
    data() {
      return {
        API_KEY: "da0cff09aa4c9440ff6429e8b20ed73c",
        url_base: "https://api.openweathermap.org/data/2.5/",
        q: "",
        weather: {},
      };
    },
    methods: {
      getWeather(e) {
        if (e.key === "Enter") {
          axios
            .get(
              `${this.url_base}weather?q=${this.q}&units=metric&APPID=${this.API_KEY}`
            )
            .then((res) => {
              return res.data;
            })
            .then(this.setResults);
        }
      },
      setResults(results) {
        this.weather = results;
      },
      dateBuilder() {
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
        return `${day}, ${date} ${month} ${year}`;
      },
    },
    components: {},
  };
</script>

<style lang="scss">
  @import url("https://fonts.googleapis.com/css2?family=Epilogue:ital,wght@0,100;0,400;1,700&display=swap");
  .container {
    background: inherit;
  }
  .weather {
    &-wrap {
      margin-top: 10rem;
      color: white;
      display: flex;
      flex-direction: column;
      align-content: center;
      align-items: center;
      .temp {
        font-size: 3rem;
        font-weight: 700;
      }
      .location {
        font-size: 1.5 rem;
        font-weight: 700;
        margin-left: 1rem;
        margin-top: 1rem;
      }
      .date {
        font-size: 0.8rem;
        font-weight: 700;
      }
      .weather-type {
        margin-top: 0.5rem;
        font-weight: 700;
      }
    }
    &-logo {
      position: absolute;
      left: 4rem;
      top: 2rem;
      color: white;
      font-weight: 700;
      font-size: 0.9rem;
      text-decoration: none;
    }
    background-attachment: fixed;
    font-family: "Epilogue", sans-serif;
    border-radius: 3px;
    box-shadow: 0px 10px 15px -3px rgba(0, 0, 0, 0.1);
    padding: 8rem 2rem;
    height: 60vh;
    width: 80vh;
    background: rgb(0, 51, 102);
    background: linear-gradient(
      90deg,
      rgba(0, 51, 102, 1) 0%,
      rgba(2, 35, 77, 1) 35%,
      rgba(3, 15, 51, 1) 100%
    );
    display: block;
    position: absolute;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    text-align: center;
    &-title {
      top: -8rem;
      position: relative;
      color: white;
      font-weight: 700;
      font-size: 0.6rem;
    }
  }
  .search-box {
    position: absolute;
    top: 1rem;
    right: 2rem;
    input {
      background-color: transparent;
      border-left: none;
      border-right: none;
      border-top: none;
      border-bottom: 2px solid #fff;
      outline: none;
      padding: 0.5rem 0.25rem;
      color: white;
      font-size: 1rem;
      font-weight: 700;
      color: white;
      font-size: 0.9rem;
      &::placeholder {
        font-weight: 700;
        color: white;
        font-size: 0.9rem;
        opacity: 0.25;
      }
      &:active,
      :focus {
        outline: none;
      }
    }
    a {
      margin-right: 2rem;
      margin-left: 1rem;
      background-color: #fff;
      padding: 0.6rem 0.65rem;
      border-radius: 30px;
      color: black;
    }
  }
</style>
