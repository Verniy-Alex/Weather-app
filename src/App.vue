<script >
import axios from "axios"

export default {
  data() {
    return {
      city: '',
      error: '',
      weatherInfo: null
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = 'Введите больше символов'
        return false
      }
      this.error = ''

      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=55bc44c0bbd63d488d098833b1c52c27`)
        .then(resp => (this.weatherInfo = resp.data))
    }

  },
  computed: {
    showTemp() {
      return 'Температура сейчас:  ' + this.weatherInfo.main.temp + '  C°';
    },
    showFeelsLike() {
      return 'Ощущается как:  ' + this.weatherInfo.main.feels_like + '  C°';
    },
    showMinTemp() {
      return 'Минимальная температура:  ' + this.weatherInfo.main.temp_min + '  C°';
    },
    showMaxTemp() {
      return 'Максимальная температура:  ' + this.weatherInfo.main.temp_max + '  C°';
    }

  }
}


</script>

<template>

  <div class="wrapper">
    <div class="weather__app">
      <h1>Погода</h1>
      <h3>Узнайте погоду в городе: {{ city }}</h3>
      <div class="inputs-block">
        <input type="text" @input="this.city = $event.target.value" placeholder="Введите название города">
        <button @click="getWeather()">Получить погоду</button>
      </div>
      <p class="error">{{ error }}</p>
      <div class="show-temp" v-if="weatherInfo != null">
        <p>{{ showTemp }}</p>
        <p>{{ showFeelsLike }}</p>
        <p>{{ showMinTemp }}</p>
        <p>{{ showMaxTemp }}</p>
      </div>
    </div>
  </div>

</template>

<style scoped>
.show-temp {
  margin-top: 40px;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.show-temp p {
  margin-top: 15px;
  border-bottom: 1px solid #333;
}

.error {
  color: darkred;
  margin-top: 15px;
}

.inputs-block {
  margin-top: 25px;
}

.inputs-block button {
  padding: 8px 10px;
  font-size: 14px;
  border: 1px solid #fff;
  color: #fff;
  background: #333;
  border-radius: 8px;
  cursor: pointer;
  transition: .2s ease-in-out;
}

.inputs-block button:hover {
  color: #333;
  background: #fff;
  border: 1px solid #333;
}

.inputs-block button:focus {
  color: #333;
  background: #fff;
  border: 1px solid #333;
}

.inputs-block input {
  width: 200px;
  padding: 8px 10px;
  background: transparent;
  border: 1px solid #333;
  border-radius: 8px;
  font-size: 14px;
  margin-right: 15px;
}

.wrapper {
  width: 1024px;
  min-width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
}

.weather__app {
  width: 600px;
  height: 400px;
  background: #fff;
  text-align: center;
  border-radius: 20px;
  border: 2px solid #333;
}

.weather__app h1 {
  margin-top: 30px;
  color: #333;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}

.weather__app h3 {
  margin-top: 15px;
  color: #333;
  font-family: system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, Oxygen, Ubuntu, Cantarell, 'Open Sans', 'Helvetica Neue', sans-serif;
}
</style>
