<script setup lang="ts">
import { defineProps } from 'vue'

type CardItemProps = {
  name: string
}
const props = defineProps<CardItemProps>()
</script>

<template>
  <div class="card-item">
    <h3>{{ name }}</h3>
  </div>
</template>

<style scoped>
.card-item {
  border: 1px solid #000;
  padding: 16px;
  border-radius: 8px;
}
</style>
