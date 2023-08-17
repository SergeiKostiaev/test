<script setup>
import TodayWeather from '../src/components/TodayWeather.vue';
import WeatherSummary from '../src/components/WeatherSummary.vue';
import { API_KEY, BASE_URL } from './constants'
import { ref, onMounted } from 'vue'

const city = ref('Paris')
const weatherInfo = ref(null)

function getWeather() {
  fetch(`${BASE_URL}?q=${city.value}&appid=${API_KEY}`)
    .then((response) => response.json())
    .then((data) => weatherInfo.value = data)
}

onMounted(getWeather)
</script>

<template>
  <div class="page">
    <main class="main">
        <div class="container">
          <div class="laptop">
            <div class="sections">
              <section class="section section-left">
                <div class="info">
                  <div class="city-inner">
                    <input 
                    v-model="city" 
                    type="text" 
                    class="search"
                    @keyup.enter="getWeather"
                    >
                  </div>
                  <WeatherSummary/>
                </div>
              </section>
              <section class="section section-right">
                <TodayWeather/>
              </section> 
            </div>
            <div class="sections">
              <section class="section-bottom">
                <div
                  class="block-bottom">
                  <div class="block-bottom-inner">
                    <div class="block-bottom-pic pic-coords"></div>
                    <div class="block-bottom-texts">
                      <div class="block-bottom-text-block">
                        <div class="block-bottom-text-block-title">
                          Долгота: 2,3488
                        </div>
                        <div class="block-bottom-text-block-desc">
                          Долгота измеряет расстояние к востоку или западу от нулевого меридиана.
                        </div>
                      </div>
                      <div class="block-bottom-text-block">
                        <div class="block-bottom-text-block-title">
                          Широта: 48,8534
                        </div>
                        <div class="block-bottom-text-block-desc">
                          Линии широты начинаются на экваторе (0 градусов широты) и идут на восток и запад параллельно экватору.
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </section>
              <section class="section-bottom">
                <div
                  class="block-bottom"
                >
                  <div class="block-bottom-inner">
                    <div class="block-bottom-pic pic-humidity"></div>
                    <div class="block-bottom-texts">
                      <div class="block-bottom-text-block">
                        <div class="block-bottom-text-block-title">
                          Влажность: 60 %
                        </div>
                        <div class="block-bottom-text-block-desc">
                          Влажность – это концентрация водяного пара, присутствующего в воздухе. Водяной пар, газообразное состояние воды, обычно невидим для человеческого глаза.
                          <br /><br />
                          Одно и то же количество водяного пара приводит к более высокой относительной влажности в холодном воздухе, чем в теплом.
                        </div>
                      </div>
                    </div>
                  </div>
                </div>
              </section>
            </div>
          </div>
        </div>
    </main>
  </div>
</template>

<style lang="sass" scoped>
@import './assets/styles/main'
.page
  position: relative
  display: flex
  justify-content: center
  align-items: center
  min-height: 100vh
  padding: 20px 0
  background-color: #59585d

.laptop
  width: 100%
  padding: 20px
  background-color: #0e100f
  border-radius: 25px

.sections
  display: flex
  width: 100%

  @media (max-width: 767px)
    flex-direction: column

.section-left
  width: 30%
  padding-right: 10px

  @media (max-width: 767px)
    width: 100%
    padding-right: 0

.section-right
  width: 70%
  padding-left: 10px

  @media (max-width: 767px)
    width: 100%
    margin-top: 16px
    padding-left: 0

.city-inner
  position: relative
  display: inline-block
  width: 100%

  &::after
    content: ''
    position: absolute
    top: 0
    right: 10px
    width: 25px
    height: 25px
    background: url('./assets/img/search.svg') no-repeat 50% 50%
    background-size: contain
    transform: translateY(50%)
    cursor: pointer

.info
  height: 100%
  padding: 16px
  background: url('./assets/img/gradient-1.jpg') no-repeat 50% 50%
  background-size: cover
  border-radius: 25px

.search
  width: 100%
  padding: 16px
  font-family: 'Inter', Arial, sans-serif
  color: $white
  background-color: rgba(0, 0, 0, 0.75)
  border-radius: 16px
  border: none
  outline: none
  cursor: pointer

.section-bottom
  width: 50%
  margin-top: 16px

  @media (max-width: 767px)
    width: 100%
</style>
