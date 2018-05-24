<template>
  <div id="root">
    <div id="scoreUser">
      Votre score est de : {{score}}
    </div>
    <div id="board"></div>
    <loose @retry="onRestart" v-if="isFinish == true"/>
  </div>
  
</template>

<script>
import board from "@/components/Board";
import Loose from "./Loose";

board.init(4);

const initBoard = () => {
  const root = document.getElementById("board");

  board.squares.forEach(column => {
    const div = document.createElement("DIV");

    root.appendChild(div);

    column.forEach(line => {
      const number = line === 0 ? "" : line;
      const span = document.createElement("DIV");

      span.innerText = number;
      if (number == "") {
        span.style.backgroundColor = "rgb(205,193,180)";
      } else if (number == 2) {
        span.style.backgroundColor = "rgb(240, 233, 226)";
      } else if (number == 4) {
        span.style.backgroundColor = "rgb(237, 224, 200)";
      } else if (number == 8) {
        span.style.backgroundColor = "rgb(242, 177, 121)";
        span.style.color = "white";
      } else if (number == 16) {
        span.style.backgroundColor = "rgb(254, 149, 99)";
        span.style.color = "white";
      } else {
        span.style.backgroundColor = "grey";
        span.style.color = "white";
      }
      div.appendChild(span);
    });
  });
};

export default {
  name: "Game",
  data() {
    return {
      score: 0,
	  msg: "Welcome to Your Vue.js App",
	  isFinish: false,
    };
  },
  components: {
    Loose
  },
  props: {

  },
  methods: {
    onRestart() {
	  this.board = new Board();
	  document.getElementById("board").innerHTML = ""
	  board.init(4)
    }
  },
  mounted() {
    initBoard();
  },
  created() {
    document.addEventListener(
      "keyup",
      event => {
        board.move(event.code.replace("Arrow", "").toLowerCase());
        document.getElementById("board").innerHTML = "";
		initBoard();
		console.log(board.isOver())
		if(board.isOver() == true){
			this.isFinish = true
		}
		else{
			this.isFinish = false
		}
      },
      false
    );
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
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
  width: 160px;
  height: 140px;
  font-size: 100px;
  padding-top: 20px;
  vertical-align: top;
  margin: 10px;
  border-radius: 10px;
}
.overlay{
	width: 100%;
	height: 100%;
	background-color: rgba(0,0,0, .5);
	position: absolute;
	z-index: 10000;
	top: 0px;
	left: 0px;
}
.tryAgain{
	position: absolute;
	margin: auto;
	top: 49%;
}
</style>
