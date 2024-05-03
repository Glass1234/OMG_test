<template>
  <div class="page">
    <div class="items">
      <div
        class="row"
        v-for="(row, rowIndex) in computedItemArr"
        :key="rowIndex"
      >
        <div v-for="(item, itemIndex) in row" :key="itemIndex" class="item">
          <span>{{ item }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref, computed } from "vue";

const itemArr = ref([]);

onMounted(() => {
  fillArray();
});

function fillArray() {
  const minRow = 100;
  const maxRow = 150;
  const minItem = 10;
  const maxItem = 25;
  const length = Math.floor(Math.random() * (maxRow - minRow + 1)) + minRow;

  itemArr.value = Array.from({ length }, (row, rowIndex) => {
    const subArrayLength =
      Math.floor(Math.random() * (maxItem - minItem + 1)) + minItem;
    return Array.from({ length: subArrayLength }, (item, itemIndex) => {
      return rowIndex * (maxItem - minItem + 1) + itemIndex;
    });
  });
}

const computedItemArr = computed(() => {
  return itemArr.value;
});
</script>

<style scoped>
.page {
  padding: 30px;
}
.items {
  display: flex;
  flex-direction: column;
  gap: 30px;
}
.row {
  background: #ececec;
  border: 1px solid #00000008;
  padding: 10px;
  display: flex;
  gap: 15px;
  border-radius: 13px;
  flex-wrap: wrap;
}
.item {
  background: #fff;
  border-radius: 4px;
  width: 70px;
  height: 70px;
  display: flex;
  flex-direction: column;
  justify-content: center;
  box-shadow: 0px 8px 14px 0px #0c0b0b1a;
  cursor: pointer;
  transition: transform 0.3s ease, filter 0.3s ease;
}
.item:hover {
  transform: scale(0.8);
  filter: opacity(0.5);
}
.item span {
  text-align: center;
}
</style>
