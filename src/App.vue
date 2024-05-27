<template>
  <div class="wrapper">
    <h1>Weather app</h1>
    <p>Check weather in {{ city == '' ? "your city" : cityName }}</p>
    <input type="text" v-model="city" placeholder="Input city">
    <button v-if="city != ''" @click="getWeather()">Get weather</button>
    <button disabled v-else>Input city name</button>
    <p class="error">{{ error }}</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      city: "",
      error: ""
    }
  },
  computed: {
    cityName() {
      return '«' + this.city + '»'
    }
  },
  methods: {
    getWeather() {
      if (this.city.trim().length < 2) {
        this.error = "Need one to enter more than one character"
        return false;
      }

      this.error = '';
    }
  }
}
</script>

<style scoped>
.error {
  color: #d03939;
}

.wrapper {
  width: 900px;
  height: 500px;
  border-radius: 50px;
  padding: 20px;
  background: #1f0f24;
  text-align: center;
  color: #fff;
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
  border-bottom: 2px solid #110813;
  color: #fcfcfc;
  font-size: 14px;
  padding: 5px 8px;
  outline: none;
}

.wrapper input:focus {
  border-bottom-color: #6e2d7d;
}

.wrapper button:disabled {
  background: #746027;
  cursor: not-allowed;
}

.wrapper button {
  background: #e3bc4b;
  color: #fff;
  border-radius: 10px;
  border: 2px solid#b99935;
  padding: 10px 15px;
  margin-left: 20px;
  cursor: pointer;
  transition: transform 500ms ease;
}

.wrapper button:hover {
  transform: scale(1.1) translateY(-3px);
}
</style>
