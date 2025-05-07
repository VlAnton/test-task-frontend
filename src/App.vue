<script setup lang="ts">
import { leftBlockData, rightBlockData } from '@/mock-data'
import CardItem from '@/components/CardItem.vue'
</script>

<template>
  <div class="page-wrapper">
    <div class="left-block">
      <div v-for="item in leftBlockData" :key="item.id">
        <CardItem :name="item.name" />
      </div>
    </div>

    <div class="right-block">
      <div v-for="item in rightBlockData" :key="item.id">
        <CardItem :name="item.name" />
      </div>
    </div>
  </div>
</template>

<style scoped>
.page-wrapper {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: space-between;
  min-height: 100vh;
  width: 100%;
  background-color: #fff;
  padding: 32px;
}
</style>
