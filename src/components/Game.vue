<template>    
  <div id="board"></div>
</template>

<script>
import board from '@/components/Board'

const initBoard = () => {
  board.init(4)

  const root = document.getElementById('board')

  board.squares.forEach((line, lIndex) => {   
    const div =  document.createElement('DIV')

    root.appendChild(div)

    line.forEach((column, cIndex) => {
      const number = column === 0 ? '' : column
      const columnNumber =  number
      const span = document.createElement('SPAN')

      span.innerText = columnNumber
      div.appendChild(span)
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
<style>
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

#board{
  width: 800px;
  height: 800px;
  border: solid 1px black;
  margin: auto;
}
div#board > div{
  width: 100%;
  height: 24.75%;
  border: solid 1px red;
}
div#board > div > span{
  width: 24.75%;
  height: 79%;
  border: solid 1px green;
  font-size: 100px;
  float: left;
  padding-top: 5%;
}
</style>
