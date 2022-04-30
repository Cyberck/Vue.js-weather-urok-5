<template>
  <div id="app" :class="weather.name != undefined && weather.main.temp > 15 ? 'hot' : '' ">
    <main>
      <div class="input-box">
        <input type="text" v-model="query" @keyup.enter="getWeather" />
      </div>
      <div class="weather" v-if="weather.name != undefined">
        <div class="location">
          {{ weather.name }}, {{ weather.sys.country }}
        </div>
        <div class="temp">{{ Math.round(weather.main.temp) }} degree</div>
        <div class="info">{{ weather.weather[0].main }}</div>
      </div>
      <div v-else>
        <p>Vi vveli ne susheshtvueshiy gorod</p>
      </div>
    </main>
  </div>
</template>


<script>
export default {
  data() {
    return {
      query: "",
      url: "https://api.openweathermap.org/data/2.5/",
      key: "88ba2f3f34d3befea68ed7301c693c0a",
      weather: {},
    };
  },
  methods: {
    getWeather() {
      fetch(`${this.url}weather?q=${this.query}&units=metric&appid=${this.key}`)
        .then((res) => res.json())
        .then((data) => {
          this.weather = data;
        });
    },
  },
};
</script>


<style scoped lang="sass">
*
  margin: 0
  padding: 0
  box-sizing: border-box

ul
  list-style: none

a
  text-decoration: none

#app
  background: url(./assets/cold-bg.jpg) no-repeat center / cover
  height: 100vh
  padding: 30px

#app.hot
  background: url(./assets/warm-bg.jpg) no-repeat center / cover

input
  display: block
  width: 100%
  padding: 15px
  border: none
  font-size: 22px
  background: rgb(166, 191, 238, 0.3)

.weather
  display: flex
  flex-direction: column
  align-items: center
  color: blue
  font-size: 40px
  row-gap: 50px
  max-width: 700px
  width: 100%
  margin: 100px auto
  padding: 50px 0
  background: rgb(184, 184, 241, 0.3)
</style>