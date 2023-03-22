<template>
  <div class="container">
    <div class="row justify-content-center">
      <div class="col-md-6">
        <div class="card my-5">
          <div class="card-body">
            <h1 class="card-title text-center mb-4">Weather Prediction</h1>
            <form @submit.prevent="getWeather">
              <div class="form-group">
                <input type="text" class="form-control" v-model="city" placeholder="Enter city name">
                <button type="submit" class="btn btn-primary btn-block">Get Weather</button>
              </div>
              
            </form>
            <div v-if="weather" class="mt-5">
              <h2 class="text-center">{{ weather.name }}, {{ weather.sys.country }}</h2>
              <div class="text-center"><p>Weather: {{ weather.weather[0].description }} </p></div>
              <div class="text-center"><p>Temperature: {{ weather.main.temp }}°C </p></div>
              <div class="text-center"><p> Feels like: {{ weather.main.feels_like }}°C </p></div>
              <div class="text-center"><p> Humidity: {{ weather.main.humidity }}% </p></div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      city: '',
      weather: null
    };
  },
  methods: {
    async getWeather() {
      const apiKey = 'bec26ff80490535a0b49345d6927c000';
      const url = `https://api.openweathermap.org/data/2.5/weather?q=${this.city}&APPID=${apiKey}&units=metric`;
      const response = await axios.get(url);
      this.weather = response.data;
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Inter:wght@400;600&display=swap');

.container {
  font-family: 'Inter', sans-serif;
  text-align: center;
  min-height: 100vh;
}

.card {
  box-shadow: 0 0 15px rgba(0,0,0,0.3);
  padding: 50px;
}

.form-control {
  border-radius: 30px;
  font-family: 'Inter', sans-serif;
  font-size: 16px;
  color: #444;
  background-color: #f2f2f2;
  border: none;
  box-shadow: none;
  padding: 20px 30px;
}

.form-control:focus {
  outline: none;
  box-shadow: none;
  border-color: #3a78a8;
}
.form-group {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
}

.btn-primary {
  border-radius: 30px;
  font-family: 'Inter', sans-serif;
  font-size: 16px;
  font-weight: 600;
  color: #fff;
  background-color: #3a78a8;
  border: none;
  padding: 16px 30px;
  transition: all 0.2s ease-in-out;
}

.btn-primary:hover {
  background-color: #326991;
  transform: translateY(-2px);
  box-shadow: 0 2px 15px rgba(0,0,0,0.2);
}

.btn-primary:focus {
  outline: none;
  box-shadow: none;
}
</style>
