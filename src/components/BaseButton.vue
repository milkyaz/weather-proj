<script setup>

</script>

<template>
  <button class="cs-button">
    <slot></slot>
  </button>
</template>

<style scoped>
.cs-button {
  width: 100%;
  border-radius: 10px;
  padding: 14px;
  font-size: 20px;
  font-weight: 600;
  height: 53px;
  border: none;
  cursor: pointer;
  display: flex;
  gap: 9px;
  align-items: center;
  justify-content: center;
  color: white;
  background: linear-gradient(
      90deg,
      #90D9E0 0%,
      #5460E6 100%
  );
}

.cs-button:hover {
  background: linear-gradient(
      90deg,
      #5460E6 0%,
      #90D9E0 100%
  );
}

</style>