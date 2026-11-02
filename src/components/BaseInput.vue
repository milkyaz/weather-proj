<script setup>
const props = defineProps(['value']);
const emit = defineEmits(['update:value']);
</script>

<template>
  <input class="cs-input" :value="props.value" @input="emit('update:value', $event.target.value)"/>
</template>

<style scoped>
.cs-input {
  color: white;
  height: 53px;
  width: 260px;
  font-size: 18px;
  padding: 15px 20px;
  border-radius: 10px;
  border: none;
  background-color: #272E37;
  box-shadow: 1px 2px 4px 0 #222831;
}

.cs-input::placeholder {
  color: #3f4958;
}
</style>