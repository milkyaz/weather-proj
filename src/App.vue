<script setup>
import State from "./components/State.vue";
import CitySelect from "./components/CitySelect.vue";
import {computed, ref} from "vue";

const API_ENDPOINT = 'https://api.weatherapi.com/v1';
const savedCity = ref('Moscow');
const data = ref();

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
  data.value = await res.json();
}
</script>

<template>
  <main class="main">
    <div id="city">{{ savedCity }}</div>
    <State v-for="item in dataModified" v-bind="item" :key="item.label" />
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