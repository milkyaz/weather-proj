<script setup>
import State from "./components/State.vue";
import CitySelect from "./components/CitySelect.vue";
import {computed, ref} from "vue";
import Error from "./components/Error.vue";
import IconSun from "./icons/weather/IconSun.vue";
import IconRain from "./icons/weather/IconRain.vue";
import IconCloud from "./icons/weather/IconCloud.vue";

const API_ENDPOINT = 'https://api.weatherapi.com/v1';
const errorMap = new Map([[1006, 'Указанный город не найден']])
const savedCity = ref('Moscow');
const data = ref();
const error = ref()

const errorDisplay = computed(() => {
  return errorMap.get(error.value?.error?.code)
})

const dataModified = computed(() => {
  if (!data.value) {
    return [];
  }
  return [
    {
      label: 'Влажность',
      stat: data.value.current.humidity + '%'
    },
    {
      label: 'Осадки',
      stat: data.value.current.chance_of_rain + '%'
    },
    {
      label: 'Ветер',
      stat: data.value.current.wind_kph + 'м/ч'
    },

  ]
})

async function getCity(city) {
  savedCity.value = city;
  const params = new URLSearchParams({
    q: city,
    lang: 'ru',
    key: '3416e0548f3f4e1185f63806262710',
    days: 3
  })
  const res = await fetch(`${API_ENDPOINT}/forecast.json?${params.toString()}`);
  if (res.status !== 200) {
    error.value = await res.json();
    data.value = null;
    return;
  }
  error.value = null;
  data.value = await res.json();
}
</script>

<template>
  <main class="main">
    <Error :error="errorDisplay"/>
    <State v-for="item in dataModified" v-bind="item" :key="item.label"/>
    <CitySelect @selected-city="getCity"/>
  </main>

</template>
<style scoped>
.main {
  display: flex;
  flex-direction: column;
  gap: 16px;
  color: white;
  background-color: #222831;
  padding: 30px 80px;
  border-radius: 20px;
}

</style>