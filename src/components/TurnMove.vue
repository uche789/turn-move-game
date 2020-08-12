<template>
  <div class="turn-move">
    <h1>Turn-move game</h1>
    <div class="buttons">
      <button @click="turn">Turn right</button>
      <button @click="move">Move forward</button>
    </div>
    <div class="Grid">
      <div class="Column" v-for="col in max" :key="col">
        <div class="Cell" v-for="cell in max" :key="cell">
          <div class="icon" :class="directionClass" v-if="visible(col, cell)">☝🏼</div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
const directionClasses =  {
  0: 'point-up',
  1: 'point-right',
  2: 'point-down',
  3: 'point-left'
};

const directions =  {
  UP: 0,
  RIGHT: 1,
  DOWN: 2,
  LEFT: 3
};

export default {
  name: 'TurnMoveGame',
  data: () => ({
    position: {
      column: 1,
      cell: 1,
    },
    direction: directions.RIGHT,
    max: 10,
  }),
  computed: {
    directionClass() {
      return directionClasses[this.direction];
    },
  },
  methods: {
    turn() {
      if (this.direction === directions.LEFT) {
        this.direction = directions.UP;
        return;
      }

      this.direction += 1;
    },

    move() {
      let newCellPosition = this.position.cell;
      let newColumnPosition = this.position.column;

      if (this.direction === directions.UP) {
        newCellPosition  -= 1;
      } else if (this.direction === directions.RIGHT) {
        newColumnPosition += 1;
      } else if (this.direction === directions.DOWN) {
        newCellPosition  += 1;
      } else if (this.direction === directions.LEFT) {
        newColumnPosition -= 1;
      }
      
      if (this.hasReachedEdge(newCellPosition, newColumnPosition)) {
        this.turn();
        return;
      }

      this.position.cell = newCellPosition;
      this.position.column = newColumnPosition;
    },
    hasReachedEdge(cellPostion, columnPostion) {
      const edgePosition = [0, 11];
      return edgePosition.includes(cellPostion) || edgePosition.includes(columnPostion);
    },
    visible(columnNumber, cellNumber) {
      return columnNumber === this.position.column && cellNumber === this.position.cell;
    } 
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.buttons {
  margin-bottom: 10px;
}

.buttons button {
  margin: 0 5px;
}

h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

.Grid {
  border: 2px solid black;
  height: 400px;
  width: 400px;
  display: flex;
  margin: auto;
  flex-direction: row;
}

.Column {
  display: flex;
  flex-direction: column;
  flex: 1;
}

.Cell {
  flex: 1;
  border: 1px solid black;
  text-align: center;
  font-size: 2em;
}

.icon {
  font-size: 24px;
}

.point-up {
  transform: rotate(0deg);
}

.point-down {
  transform: rotate(180deg);
}

.point-right {
  transform: rotate(90deg);
}

.point-left {
  transform: rotate(-90deg);
}
</style>
