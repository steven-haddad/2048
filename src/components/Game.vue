<template>
  <div id="root">
    <div id="scoreUser">
      Votre score est de : {{score}}
    </div>
    <div id="board">
      <div v-for="(column, cIndex) in board.squares"
        :key="cIndex">
        <div :class="getTileColor(line)" v-for="(line, lIndex) in column" :key="lIndex">{{ line === 0 ? '' : line }}</div>
      </div>
    </div>
    <div>
    Nombre de carrés :
    <select v-model="selectList" id="selectListNumberSquare" @change="changeGameModes">
      <option value="4" selected>4</option>
      <option value="5">5</option>
      <option value="6">6</option>
    </select>
    </div>
    <loose @restart="onRestart" v-if="board.over == true"/>
  </div>
  
</template>

<script>
import Board from "@/components/Board"
import Loose from "@/components/Loose"
import http from "@/utils/http"

export default {
  name: "Game",
  data() {
    return {
      board: {},
      score: 0,
      msg: "Welcome to Your Vue.js App",
      selectList: 4,
      startTime: null,
      endTime: null,
    }
  },
  components: {
    Loose
  },
  props: {},
  methods: {
    initializeBoard (boardLength) {
      this.board = Board
      this.startTime = new Date()
      if (!boardLength) {
        this.board.init(4)
      } else {
        this.board.init(boardLength)
      }
    },
    getTileColor(tileValue) {
      let className = ''

      if (tileValue == '') {
        className = 'empty-tile'
      } else if (tileValue == 2) {
        className = 'two-tile'
      } else if (tileValue == 4) {
        className = 'four-tile'        
      } else if (tileValue == 8) {
        className = 'eight-tile'
      } else if (tileValue == 16) {
        className = 'sixteen-tile'
      } else {
        className = 'big-tile'        
      }

      return className
    },
    launchAI(){
      let position = ["up", "down", "left", "right"]

    const ia = isFinish => {
      setTimeout(() => {  
        if (isFinish) {
          this.endTime = new Date()

          const time = (Number(this.endTime) - Number(this.startTime)) / 1000
          const name = '[IA] DiDier'

          http
            .get(`${name}/${this.score}/${time}`)
            .then(response => console.log('success: ', response))
            .catch(error => console.error('error: ', error))
        }
        else {
          this.board.move(position[Math.floor(Math.random() * position.length)])

          this.$forceUpdate()
          this.score = this.board.points
          ia(this.board.over)
        }
      }, 10)
    }

    ia(this.board.over)
    },
    onRestart() {
      this.$forceUpdate()
      this.initializeBoard()
      this.launchAI()
    },
    changeGameModes() {
      this.$forceUpdate()      
      this.score = 0
      this.initializeBoard(this.selectList)
    },
    setStartTime () {
      this.startTime = new Date()
    }
  },
  mounted() {
    this.launchAI()
  },
  created() {
    this.initializeBoard()
    this.setStartTime()
    document.addEventListener(
      "keyup",
      event => {
        this.board.move(event.code.replace("Arrow", "").toLowerCase())
        this.$forceUpdate()
        this.score = this.board.points
      },
      false
    )
  }
}
</script>

<style>
h1,
h2 {
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

#scoreUser {
  font-size: 40px;
}

#board {
  border: solid 1px rgb(187, 173, 160);
  padding: 20px;
  display: inline-block;
  background-color: rgb(187, 173, 160);
}
#board > div {
  display: inline-block;
  vertical-align: top;
}
div#board > div > div {
  width: 100px;
  height: 75px;
  font-size: 40px;
  padding-top: 25px;
  vertical-align: top;
  margin: 10px;
  border-radius: 10px;
}
.overlay {
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  position: absolute;
  z-index: 10000;
  top: 0px;
  left: 0px;
  text-align: center;
}
.tryAgain {
  position: absolute;
  top: 49%;
}
.empty-tile {
  background-color: rgb(205,193,180);
}
.two-tile {
  background-color: rgb(240, 233, 226);
}
.four-tile {
  background-color: rgb(237, 224, 200);
}
.eight-tile {
  color: white;
  background-color: rgb(242, 177, 121);
}
.sixteen-tile {
  color: white;
  background-color: rgb(254, 149, 99);
}
.big-tile {
  color: white;
  background-color: grey;
}

</style>