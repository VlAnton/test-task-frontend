<script setup lang="ts">
import { ref, reactive } from 'vue'
import { leftBlockData, rightBlockData } from '@/mock-data'
import CardItem from '@/components/CardItem.vue'

type Item = {
  id: number
  name: string
}

const leftBlockSelected = reactive<Item[]>([])
const rightBlockSelected = ref<Item | null>(null)

const isSelected = (item: Item) => {
  return Boolean(leftBlockSelected.find((selectedItem) => selectedItem.id === item.id))
}

const onToggleLeftBlock = (item: Item) => {
  const index = leftBlockSelected.findIndex((selectedItem) => selectedItem.id === item.id)
  if (index !== -1) {
    leftBlockSelected.splice(index, 1)
  } else if (leftBlockSelected.length < 6) {
    leftBlockSelected.push(item)
  } else {
    leftBlockSelected.pop()
    leftBlockSelected.push(item)
  }
}
const onToggleRightBlock = (item: Item) => {
  if (rightBlockSelected.value?.id === item.id) {
    rightBlockSelected.value = null
  } else {
    rightBlockSelected.value = item
  }
}
</script>

<template>
  <main class="page-wrapper">
    <section class="selected-items-section">
      <div class="selected-left-block">
        <div v-for="item in leftBlockSelected" :key="item.id" class="card-item-wrapper">
          <CardItem :name="item?.name" />
        </div>
        <p class="selected-counter">Selected {{ leftBlockSelected.length }}/6</p>
      </div>

      <div class="selected-right-block">
        <CardItem :name="rightBlockSelected?.name" lg />
      </div>
    </section>
    <section class="items-section">
      <div class="items-block">
        <div v-for="item in leftBlockData" :key="item.id" class="card-item-wrapper">
          <CardItem
            :name="item.name"
            @click="onToggleLeftBlock(item)"
            :selected="isSelected(item)"
          />
        </div>
      </div>

      <div class="items-block">
        <div v-for="item in rightBlockData" :key="item.id" class="card-item-wrapper">
          <CardItem
            :name="item.name"
            @click="onToggleRightBlock(item)"
            :selected="item.id === rightBlockSelected?.id"
          />
        </div>
      </div>
    </section>
  </main>
</template>

<style scoped>
.page-wrapper {
  display: flex;
  flex-direction: column;
  align-items: center;
  min-height: 100vh;
  width: 100vw;
  background-color: #fff;
  padding: 32px;
  gap: 32px;
}

.selected-items-section,
.items-section {
  display: flex;
  flex-direction: row;
  width: 100%;
  gap: 32px;
}

.selected-items-section {
  justify-content: space-between;
  height: 100%;
}

.items-block {
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(200px, 1fr));
  gap: 32px;
  width: 100%;
  min-height: 50vh;
  border: 1px solid #000;
  padding: 16px;
  border-radius: 8px;
}

.selected-left-block {
  position: relative;
  display: grid;
  max-width: calc(25vw - 32px);
  grid-template-columns: repeat(auto-fill, minmax(100px, 1fr));
  gap: 32px;
  width: 100%;
  min-height: 25vh;
  height: 100%;
  border: 1px solid #000;
  padding: 16px;
  padding-bottom: 48px;
  border-radius: 8px;
}

.selected-counter {
  position: absolute;
  bottom: -2px;
  left: 16px;
  font-size: 14px;
  color: #000;
}

.selected-right-block {
  min-width: calc(25vw - 32px);
}

@media screen and (min-width: 3812px) {
  .card-item-wrapper {
    max-height: 200px;
  }
}
</style>
