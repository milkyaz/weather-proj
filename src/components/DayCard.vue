<script setup>
import IconSun from "../icons/weather/IconSun.vue";
import IconCloud from "../icons/weather/IconCloud.vue";
import IconRain from "../icons/weather/IconRain.vue";

const {weatherCode, date, temp} = defineProps({
  weatherCode: Number,
  date: Date,
  temp: String,
})

const iconMap = {
  1000: IconSun,
  1006: IconCloud,
  1009: IconRain,
}

</script>

<template>
  <button class="day-card">
    <component :is="iconMap[weatherCode]" />
    <span class="day-card__text">{{ date.toLocaleDateString('ru-Ru', {weekday: 'short'}) }}</span>
    <span class="day-card__temp">{{ temp + "°C" }}</span>
  </button>
</template>

<style scoped>
.day-card {
  cursor: pointer;
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 15px 24px;
  gap: 15px;
  background-color: #272E37;
  border-radius: 10px;
  border: none;
  color: white;
}

.day-card__text {
  font-size: 20px;
}

.day-card__temp {
  font-size: 20px;
  font-weight: bold;
}

.day-card:hover {
  background-color: #3A434F;
}

</style>