<template>
    <div class="game-of-life">
      <div
        class="grid"
        :style="{ gridTemplateColumns: 'repeat(' + cols + ', 20px)' }">
        <div
          v-for="(cell, index) in cells"
          :key="index"
          :class="{ 'cell-alive': cell }"
          @click="toggleCell(index)"
          class="cell">
        </div>
      </div>
      <button @click="nextGeneration">Prochaine Génération</button>
      <button @click="reset">Réinitialiser</button>
    </div>
  </template>
  
  <script>
  export default {
    
    data() {
      return {
        rows: 30,
        cols: 30,
        cells: Array(900).fill(false) // 30x30 grid
      };
    },
    name: 'GameOfLife',
    methods: {
      toggleCell(index) {
        this.cells[index] = !this.cells[index];
      },
    nextGeneration() {
        const newCells = this.cells.slice();
  for (let i = 0; i < this.cells.length; i++) {
    const x = i % this.cols;
    const y = Math.floor(i / this.cols);
    const neighbors = [
      this.cells[((y - 1 + this.rows) % this.rows) * this.cols + ((x - 1 + this.cols) % this.cols)],
      this.cells[((y - 1 + this.rows) % this.rows) * this.cols + x],
      this.cells[((y - 1 + this.rows) % this.rows) * this.cols + ((x + 1) % this.cols)],
      this.cells[y * this.cols + ((x - 1 + this.cols) % this.cols)],
      this.cells[y * this.cols + ((x + 1) % this.cols)],
      this.cells[((y + 1) % this.rows) * this.cols + ((x - 1 + this.cols) % this.cols)],
      this.cells[((y + 1) % this.rows) * this.cols + x],
      this.cells[((y + 1) % this.rows) * this.cols + ((x + 1) % this.cols)]
    ].filter(Boolean).length;

    const alive = this.cells[i];
    if (alive && (neighbors < 2 || neighbors > 3)) newCells[i] = false;
    else if (!alive && neighbors === 3) newCells[i] = true;
  }
  this.cells = newCells;
    },
    reset() {
        this.cells.fill(false);
      }
    }
  };
  </script>
  
  <style scoped>
  .grid {
    display: grid;
  }
  .cell {
    width: 20px;
    height: 20px;
    border: 1px solid #ccc;
    background-color: #fff;
  }
  .cell-alive {
    background-color: black;
  }
  </style>
  