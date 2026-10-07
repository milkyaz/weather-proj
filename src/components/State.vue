<script setup>

const {label, stat} = defineProps({
  label: String,
  stat: String
})
</script>

<template>
  <div class="cs-state">
    <div class="cs-state__name"> {{ label }}</div>
    <div class="cs-state__value"> {{ stat }}</div>
  </div>
</template>

<style scoped>
.cs-state {
  font-size: 28px;
  display: flex;
  gap: 72px;
  justify-content: space-between;
}

</style>