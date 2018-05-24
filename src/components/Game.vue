<template>    
  <div id="board"></div>
</template>

<script>
import board from '@/components/Board'

const initBoard = () => {
  board.init(4)

  const root = document.getElementById('board')

  board.squares.forEach((line, lIndex) => {    
    root.appendChild(document.createElement('DIV'))

    line.forEach((column, cIndex) => {
      const number = column === 0 ? '' : column
      const columnNumber =  document.createTextNode(number)
      const span = document.createElement('SPAN').appendChild(columnNumber)

      root.appendChild(span)
    })
  })
}

export default {
  name: 'Game',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  methods: {
    onRestart(){
      this.board = new Board()
    }      
  },
  mounted () {
    initBoard()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h1, h2 {
  font-weight: normal;
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
</style>
