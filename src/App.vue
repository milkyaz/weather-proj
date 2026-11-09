<script setup>
import State from "./components/State.vue";
import CitySelect from "./components/CitySelect.vue";
import {computed, ref} from "vue";
import Error from "./components/Error.vue";
import DayCard from "./components/DayCard.vue";

const API_ENDPOINT = 'https://api.weatherapi.com/v1';
const errorMap = new Map([[1006, 'Указанный город не найден']])
const savedCity = ref('Moscow');
const data = ref();
const error = ref();
const days = ref();

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
  days.value = data.value.forecast.forecastday;
}
</script>

<template>
  <main class="main">
    <Error :error="errorDisplay"/>
    <div v-if="data" class="stat">
      <div class="stat-list">
        <State v-for="item in dataModified" v-bind="item" :key="item.label"/>
      </div>
      <div class="day-card__list">
        <DayCard v-for="item in days"
                 :key="item.date"
                 :weather-code="item.day.condition.code"
                 :temp="item.day.maxtemp_c"
                 :date="new Date(item.date)"
        />
      </div>
    </div>
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

.day-card__list {
  display: flex;
  gap: 1px;
}

.stat {
  display: flex;
  flex-direction: column;
  gap: 80px;
  margin-bottom: 70px;
}

.stat-list {
  display: flex;
  flex-direction: column;
  gap: 16px;
}
</style>