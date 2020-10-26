<template>
  <div class="container">
    <section class="sidebar">
    <!-- <form class="form">
        <select v-model="location" class="form__select" name="location" id="location">
          <option v-for="city in cities" :key="city" v-bind:value="city">{{city}}</option>
        </select>
        <input class="form__button" type="submit" value="Search">
      </form> -->
      <WeatherForm />
      <div class="widget">
        <p class="widget__temp">{{temperature}}<span class="widget__temp--celcius">ºC</span></p>
        <p class="widget__date">{{date}}</p>
        <h2 class="widget__location"><i class="material-icons icon">location_on</i> <span class="widget__location-text">{{location}}</span></h2>
        <p class="error">{{error}}</p>
    </div>
    </section>
    <main class="main">
    </main>
    
  </div>
</template>

<script>
import axios from "axios";
import moment from "moment";
import WeatherForm from "./components/WeatherForm.vue";

//Convert Kelvin in Celcius, needed due to the api return temperature in Kelvin

export default {
  name: "App",
  mounted() {
    //Called on first rendering
    this.getData();
  },
  components: {
    WeatherForm
  },
  computed: {
    temperature: function() {
      return Math.floor(this.temp - 273.15);
    },
    date: function() {
      let dateString = moment.unix(this.unix);
      return dateString.locale("fr").format("LL");
    },
    weatherIcon: function() {
      return null;
    }
  },
  methods: {
    getData: function() {
      //this method is called when we need to retrieve the weather data
      //for a precise location
      axios
        .get(
          `http://api.openweathermap.org/data/2.5/weather?q=${
            this.location
          }&appid=d8226f44f17257daa0c78241180a1474`
        )
        .then(
          response => {
            //Set the new weather data to data local state
            this.data = response.data;
            this.unix = response.data.dt;
            this.temp = response.data.main.temp;
            this.weatherId = response.data.weather[0].id.toString().slice(0, 1);
            this.error = null;
          },
          () => {
            this.error = "Impossible de récupérer la méteo";
          }
        );
    }
  },
  data() {
    return {
      location: "paris",
      error: null,
      data: null,
      temp: 273.15,
      unix: null,
      weatherId: null,
      cities: ["paris", "nice", "lyon", "rennes"]
    };
  }
};
</script>

<style>
.container {
  box-sizing: border-box;
  overflow: auto;
  height: 100vh;
  width: 100vw;
  background-color: #1e213a;
  color: #e7e7eb;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
}

.sidebar {
  grid-column-start: 1;
  grid-column-end: 5;
  display: flex;
  align-items: center;
  flex-direction: column;
  padding: 0 46px;
}

.main {
  grid-column-start: 5;
  grid-column-end: -1;
  background: #100e1d;
}

/* .form {
  width: 100%;
  display: flex;
  justify-content: flex-start;
  padding-top: 40px;
}

.form__button {
  height: 64px;
  width: 30%;
  font-size: 16px;
  background-color: #3c47e9;
  border: 1px solid #3c47e9;
  color: #e7e7eb;
  cursor: pointer;
}

.form__select {
  display: inline-block;
  width: 70%;
  height: 64px;
  border: 1px solid #616475;
  padding-left: 12px;
  font-size: 16px;
  background: #1e213a;
  color: #e7e7eb;
  appearance: none;
  -moz-appearance: none;
  -webkit-appearance: none;
}

option {
  height: 64px;
  text-transform: uppercase;
} */

.widget {
  grid-column-start: 1;
  grid-column-end: 5;
  display: flex;
  align-items: center;
  /* justify-content: space-around; */
  flex-direction: column;
  padding: 0 46px;
}

.widget__location {
  font-weight: 600;
  font-size: 18px;
  line-height: 21px;
  color: #88869d;
}

.widget__location-text {
  text-transform: capitalize;
}

i {
  vertical-align: bottom;
}

.widget__date {
  font-weight: 500;
  font-size: 18px;
  line-height: 21px;
  color: #88869d;
}
.widget__temp {
  font-weight: 500;
  font-size: 144px;
  line-height: 169px;
}

.widget__temp--celcius {
  font-size: 80px;
  color: #88869d;
}
</style>
