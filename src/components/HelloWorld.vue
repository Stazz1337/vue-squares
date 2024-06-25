<template>
  <RecycleScroller
    :items="rows"
    :item-size="60"
    class="scroller"
    v-slot="{ item: row, index: rowIndex, active }"
  >
        <div class="row">
          <div
            v-for="(square, squareIndex) in row.squares"
            :key="`${row.id}-${squareIndex}`"
            class="square"
            :style="{
              borderRadius: `${square.borderRadius}px`,
            }">
            {{ square.value }}
          </div>
        </div>
  </RecycleScroller>
</template>
  

<script setup>
import { ref, onMounted } from 'vue';
import { RecycleScroller  } from 'vue-virtual-scroller'
import 'vue-virtual-scroller/dist/vue-virtual-scroller.css'

const rows = ref([]);

onMounted(() => {
    generateData();
});

function generateData() {
    rows.value = [];
    const maxRows = 100000;
    const minSquaresPerRow = 10;
    const maxSquaresPerRow = 20;

    for (let i = 0; i < maxRows; i++) {
        const squaresCount =
            Math.floor(Math.random() * (maxSquaresPerRow - minSquaresPerRow + 1)) +
            minSquaresPerRow;
        const row = {
            id: i,
            squares: [],
        };
        for (let j = 0; j < squaresCount; j++) {
            const borderRadius = Math.floor(Math.random() * 51);
            const value = Math.floor(Math.random() * 101);
            row.squares.push({ borderRadius, value });
        }
        rows.value.push(row);
    }
}
</script>

<style scoped>

.scroller{
    width: 100%;
    height: 100vh;
    overflow: auto;
    display: flex;
    flex-direction: row;
    gap: 5px;
    padding: 5px;
  }

.row {
    display: flex;
    flex-direction: row;
    gap: 5px;
    margin-bottom: 5px;
    height: 50px;
    width: 100%;
}

.square {
    display: flex;
    justify-content: center;
    align-items: center;
    width: 50px;
    height: 50px;
    border: 1px solid black;
}

.square:hover {
    transform: scale(0.8);
}
</style>
