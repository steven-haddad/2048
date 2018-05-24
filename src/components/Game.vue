<template>
  <div id="root">
    <div id="scoreUser">
      Votre score est de : {{score}}
    </div>
    <div id="board"></div>
  </div>
  
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
      const span = document.createElement('SPAN')

      span.innerText = number
      if(number == ''){
        span.style.backgroundColor = 'rgb(205,193,180)'
      }
      else if(number == 2){
        span.style.backgroundColor = 'rgb(240, 233, 226)'
      }
      else if(number == 4){
        span.style.backgroundColor = 'rgb(237, 224, 200)'
      }
      else if(number == 8){
        span.style.backgroundColor = 'rgb(242, 177, 121)'
        span.style.color = 'white'
      }
      else if(number == 16){
        span.style.backgroundColor = 'rgb(254, 149, 99)'
        span.style.color = 'white'
      }
      div.appendChild(span)
    })
  })
}

export default {
  name: 'Game',
  data () {
    return {
      score: 0,
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
  border: solid 1px rgb(187, 173, 160);
  padding: 20px;
  display: inline-block;
  background-color: rgb(187, 173, 160);
}
div#board > div > span{
  width: 160px;
  height: 140px;
  font-size: 100px;
  display: inline-block;
  padding-top: 20px;
  vertical-align: top;
  margin: 10px;
  border-radius: 10px;
}
</style>
