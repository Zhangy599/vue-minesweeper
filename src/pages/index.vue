<script setup lang="ts">
interface BlockState {
  x: number
  y: number
  revealed?: boolean
  mine?: boolean
  flagged?: boolean
  adjacentMines?: number
}
const WIDTH = 10
const HEIGHT = 10
const state = reactive(Array.from({ length: HEIGHT }, (_, y) => {
  return Array.from({ length: WIDTH }, (_, x): BlockState => ({
    x, y,
  }))
}))
function onClick(x: number, y: number) {
  console.log(x, y)
}

function generateMines() {
  for (const row of state) {
    for (const block of row)
      block.mine = Math.random() < 0.3
  }
}
generateMines()
</script>

<template>
  <div>
    Minesweeper
    <div v-for="row, y in state" :key="y">
      <button
        v-for="item, x in row"
        :key="x"
        w-8
        y-8
        border="~"
        hover:bg-gray
        @click="onClick(x, y)"
      >
        {{ item.mine ? 'x' : '1' }}
      </button>
    </div>
  </div>
</template>
