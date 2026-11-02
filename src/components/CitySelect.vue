<script setup>
import BaseButton from "./BaseButton.vue";
import {onMounted, ref} from "vue";
import BaseInput from "./BaseInput.vue";

const emit = defineEmits(['selectedCity']);
let isEdited = ref(false);
let city = ref('Moscowdw');

function select() {
  isEdited.value = false;
  emit('selectedCity', city.value);
}

function edit() {
  isEdited.value = true;
}

function updateCity(newCity) {
  city.value = newCity;
}

onMounted(() => {
  emit('selectedCity', city.value);
})
</script>

<template>
  <div class="city-select">
    <div v-if="!isEdited">
      <BaseButton @click="edit">
        <img src="../assets/location.svg" alt="location">
        Изменить город
      </BaseButton>
    </div>
    <div v-if="isEdited" class="city-select__form">
      <BaseInput placeholder="Введите город" :value="city" @update:value="updateCity" @keyup.enter="select" />
      <BaseButton @click="select">Сохранить</BaseButton>
    </div>
  </div>
</template>

<style scoped>
.city-select {
  width: 420px;
}

.city-select__form {
  display: flex;
  gap: 12px;

}

</style>