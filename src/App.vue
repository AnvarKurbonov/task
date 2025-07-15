
<template>
  <div class="container">
    <div class="top">
      <div class="block">
      <!-- Верх слева -->
       <div class="block-header">SELECTED ITEM</div>
        <div class="selected-list">
          <div
            v-for="id in selectedItems"
            :key="id"
            class="item"
          >
            {{ getItemName(id) }}
          </div>
        </div>
        <div class="counter">selected: {{ selectedItems.length }} / 6</div>
      </div>

      <div class="block">
        <!-- Верх справа -->
        <div class="block-header">SELECTED ITEM</div>
        <div class="selected-list">
          <div v-if="selectedSingle !== null" class="item">
            {{ getSecondaryItemName(selectedSingle) }}
          </div>
          <div v-else class="empty">—</div>
        </div>
      </div>
    </div>

    <div class="bottom">
      <div class="block">
        <!-- Низ слева -->
        <div class="item-list">
          <div
            v-for="item in items"
            :key="item.id"
            class="item"
            :class="{ selected: selectedItems.includes(item.id) }"
            @click="toggleItem(item.id)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
      <div class="block">
        <!-- Низ справа -->
        <div class="item-list">
          <div
            v-for="item in secondaryItems"
            :key="item.id"
            class="item"
            :class="{ selected: selectedSingle === item.id }"
            @click="selectSingle(item.id)"
          >
            {{ item.name }}
          </div>
        </div>
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
import { ref } from 'vue'

const items = [
  { id: 1, name: 'Shoes 1' },
  { id: 2, name: 'Shoes 2' },
  { id: 3, name: 'Shoes 3' },
  { id: 4, name: 'Shoes 4' },
  { id: 5, name: 'T-shirt 1' },
  { id: 6, name: 'T-shirt 2' },
  { id: 7, name: 'T-shirt 3' },
  { id: 8, name: 'T-shirt 4' },
]

const secondaryItems = [
  { id: 11, name: 'Jacket 1'},
  { id: 12, name: 'Jacket 2'},
  { id: 13, name: 'Jacket 3'},
  { id: 14, name: 'Jacket 4'},
  { id: 15, name: 'Hoodie 1'},
  { id: 16, name: 'Hoodie 2'},
  { id: 17, name: 'Hoodie 3'},
  { id: 18, name: 'Hoodie 4'},
]

const selectedItems = ref<number[]>([])
const selectedSingle = ref<number | null>(null)

function selectSingle(id: number) {
  if (selectedSingle.value === id) {
    selectedSingle.value = null
  } else {
    selectedSingle.value = id
  }
}

function getSecondaryItemName(id: number): string {
  const item = secondaryItems.find((item) => item.id === id)
  return item ? item.name : 'Неизвестно'
}

function toggleItem(id: number) {
  const index = selectedItems.value.indexOf(id)
  if (index > -1) {
    selectedItems.value.splice(index, 1)
  } else if (selectedItems.value.length < 6) {
    selectedItems.value.push(id)
  }
}

function getItemName(id: number): string {
  const item = items.find((item) => item.id === id)
  return item ? item.name : 'Незвестно'
}

</script>
