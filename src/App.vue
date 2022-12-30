<script>
import axios from 'axios'

export default {
    data() {
      return {
        city: "",
        error: "",
        info: null,
      }
    },
    computed: {
      cityName() {
        return "\"" + this.city + "\"";
      }
    },
    methods: {
      getWeather() {
        if (this.city.trim().length < 2) {
          this.error = "Нужно более длинное название";
          return false;
        }

        this.error = "";

        axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&units=metric&appid=9cb5c472ba98892cc7eb15a8de11a182`)
            .then(res => (this.info = res.data));
      }
    }
}
</script>

<template>
  <div class="wrapper">
    <h1>Погодное приложения</h1>
    <p>Узнать погоду в {{ city == "" ? "вашем городе" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Введите город">
    <button v-if="city != ''" @click="getWeather()">Получить погоду</button>
    <button v-else disabled>Введите название города</button>
    <p class="error">{{ error }}</p>

    // TODO: доделать вывод
    <p v-show="info != null">{{ info.main }}</p>

  </div>
</template>

<style scoped>

  .error {
    color: #bb3131;
  }

  .wrapper {
    width: 900px;
    height: 500px;
    border-radius: 50px;
    padding: 20px;
    background: #332892;
    text-align: center;
    color: white;
  }
  .wrapper h1 {
    margin-top: 50px;
  }

  .wrapper p {
    margin-top: 20px;
  }

  .wrapper input {
    margin-top: 30px;
    background: transparent;
    border: 0;
    border-bottom: 2px solid #a39ce4;
    color: white;
    font-size: 14px;
    padding: 5px 8px;
    outline: none;
  }

  .wrapper input:focus {
    border-bottom-color: darkmagenta;
  }

  .wrapper button:disabled {
    background: #865a30;
    cursor: not-allowed;
  } 

  .wrapper button {
    background: #db9451;
    color: white;
    border-radius: 10px;
    border: 2px solid #b99935;
    padding: 10px 15px;
    margin-left: 20px;
    cursor: pointer;
    transition: transform 250ms ease;
  }

  .wrapper button:hover {
    transform: scale(0.95);
  }

</style>
