<script setup>
import BaseButton from "./BaseButton.vue";
import {ref} from "vue";

const emit = defineEmits(['selectedCity']);
let isEdited = ref(false);

function select() {
  isEdited.value = false;
  emit('selectedCity', 'London');
}

function edit() {
  isEdited.value = true;
}

</script>

<template>
  <BaseButton @click="edit">
    <img src="../assets/location.svg" alt="location">
    Изменить город
  </BaseButton>
  <div v-if="isEdited">
    <input />
    <BaseButton @click="select">Сохранить</BaseButton>
  </div>

</template>

<style scoped>

</style>