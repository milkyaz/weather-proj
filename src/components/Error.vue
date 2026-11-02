<script setup>
const props = defineProps({
  error: String,
})
</script>

<template>
<div class="error" v-if="props.error">{{ props.error }}</div>
</template>

<style scoped>
.error {
  font-size: 18px;
  padding: 15px;
  text-align: center;
  background-color: #272E37;
  border-radius: 0 0 25px 25px;
  margin-top: -30px;
  margin-bottom: 30px;
}

</style>