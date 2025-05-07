<script setup>
import { defineProps } from "vue";

const props = defineProps<{ title: string }>();
</script>

<template>
  <div class="card-item">
    <h3>{{ title }}</h3>
  </div>
</template>

<style scoped>
.card-item {
  border: 1px solid #000;
  padding: 16px;
  border-radius: 8px;
}
</style>
