<script setup lang="ts">
import { defineProps, computed } from 'vue'

type CardItemProps = {
  name?: string
  lg?: boolean
  selected?: boolean
}
const props = defineProps<CardItemProps>()
const fontSize = computed(() => (props.lg ? '40px' : '14px'))
const bgColor = computed(() => (props.selected ? '#f0f0f0' : '#fff'))
</script>

<template>
  <div class="card-item">
    <h3>{{ props.name }}</h3>
  </div>
</template>

<style scoped>
.card-item {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #000;
  padding: 16px;
  border-radius: 8px;
  cursor: pointer;
  height: 100%;
  width: 100%;
  background-color: v-bind(bgColor);
}

.card-item h3 {
  font-size: v-bind(fontSize);
  margin: 0;
}

.card-item:hover {
  background-color: #f0f0f0;
}
</style>
