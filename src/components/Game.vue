<template>    
 
<div class="board"  tabIndex="1">
       
</div>



</template>

<script>

import Board from '@/Board'
import Cell from './Cell.vue'


Board.init(4)
console.log(Board);



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
