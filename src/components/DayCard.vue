<script setup>
import IconSun from "../icons/weather/IconSun.vue";
import IconCloud from "../icons/weather/IconCloud.vue";
import IconRain from "../icons/weather/IconRain.vue";
import {computed} from "vue";

const {weatherCode, date, temp, isActive} = defineProps({
  weatherCode: Number,
  date: Date,
  temp: String,
  isActive: Boolean
})
const iconColor = computed(() => isActive ? '#000000' : '#FFFFFF');
</script>

<template>
  <button class="day-card" :class="{active: isActive}">
    <IconSun v-if="weatherCode <= 1003" :color="iconColor"/>
    <IconCloud v-if="weatherCode >= 1006 && weatherCode < 1063" :color="iconColor"/>
    <IconRain v-if="weatherCode >= 1063" :color="iconColor"/>
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

.active {
  background-color: #FFFFFF;
  color: #000000;
}

.day-card__text {
  font-size: 20px;
}

.day-card__temp {
  font-size: 20px;
  font-weight: bold;
}

.day-card:not(.active):hover {
  background-color: #3A434F;
}

</style>