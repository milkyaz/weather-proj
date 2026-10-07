<script setup>
import State from "./components/State.vue";
import CitySelect from "./components/CitySelect.vue";
import {computed, ref} from "vue";

const savedCity = ref('Moscow');
const data = ref({
  humidity: 20,
});

const dataModified = computed(() => {
  return {
    label: 'Влажность',
    stat: data.value.humidity + '%'
  }
})

async function getCity(city) {
  savedCity.value = city;
  data.value.humidity = 20;
}
</script>

<template>
  <main class="main">
    <div id="city">{{ savedCity }}</div>
    <State v-bind="dataModified" />
    <State label="Осадки" stat="0%"/>
    <CitySelect @selected-city="getCity" />
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