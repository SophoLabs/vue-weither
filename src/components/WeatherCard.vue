<template>
  <div class="weather-card glass">
    <div class="weather-info" v-if="info">
      <h2 class="text-3xl font-bold">{{ info.name }}, {{ info.sys.country }}</h2>
      <h2 class="text-2xl font-bold">{{ time }}</h2>
      <span class="text-xl font-bold">{{ Math.floor(info.main.temp) }}C</span>
      <span class="text-lg font-bold">Real Feel {{ Math.floor(info.main.feels_like) }}C</span>
      <span class="text-lg">Humidity {{ info.main.humidity }}%</span>
    </div>
    <div class="weather-icon">{{ checkClouds }}</div>
  </div>
</template>

<script>

export default {
  props: ['info'],
  data() {
    return {
      time: null,
    };
  },
  watch: {
    info(value) {
      this.time = new Date((value.sys.sunrise + value.timezone) * 1000).toLocaleDateString()
    }
  },
  computed: {
    checkClouds() {
      switch (this.info.weather[0].main) {
        case 'Rain':
          return '🌧';
        case 'Clouds':
          return '⛅';
        case 'Clear':
          return '🌤'
        default:
          return '🌤'
      }
    }
  },
  mounted() {
    console.log(this.$props)
  }


};
</script>

<style lang="scss">
.weather-card {
  align-content: center;
  margin: 0 auto;
  padding: 105px;
  display: flex;
  width: 550px;
  justify-content: space-between;
  .weather-info {
    display: flex;
    justify-content: center;
    flex-direction: column;
    .date {
      font-size: 2rm;
    }
  }
  .weather-icon {
    font-size: 150px;
  }
}
.glass {
  margin-top: 30px;
  color: #fff;
  /* From https://css.glass */
  padding: 16px;
  background: rgba(255, 255, 255, 0.2);
  border-radius: 16px;
  box-shadow: 0 4px 30px rgba(0, 0, 0, 0.1);
  backdrop-filter: blur(5px);
  -webkit-backdrop-filter: blur(5px);
  border: 1px solid rgba(255, 255, 255, 0.3);
}
</style>
