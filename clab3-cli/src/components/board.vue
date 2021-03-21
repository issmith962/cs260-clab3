<template>
  <div class="board">
		<div id="container">
			<div class="row">
				<div class="move-box" id="box-0" v-on:click="makeMove(0)">
					<img v-show="show.box0" :src="boxes.box0" alt=" "/>
				</div>
				<div class="move-box" id="box-1" v-on:click="makeMove(1)">
					<img v-show="show.box1" :src="boxes.box1" alt=" "/>
				</div>
				<div class="move-box" id="box-2" v-on:click="makeMove(2)">
					<img v-show="show.box2" :src="boxes.box2" alt=" "/>
				</div>
			</div>
			<div class="row">
				<div class="move-box" id="box-3" v-on:click="makeMove(3)">
					<img v-show="show.box3" :src="boxes.box3" alt=" "/>
				</div>
				<div class="move-box" id="box-4" v-on:click="makeMove(4)">
					<img v-show="show.box4" :src="boxes.box4" alt=" "/>
				</div>
				<div class="move-box" id="box-5" v-on:click="makeMove(5)">
					<img v-show="show.box5" :src="boxes.box5" alt=" "/>
				</div>
			</div>
			<div class="row">
				<div class="move-box" id="box-6" v-on:click="makeMove(6)">
					<img v-show="show.box6" :src="boxes.box6" alt=" "/>
				</div>
				<div class="move-box" id="box-7" v-on:click="makeMove(7)">
					<img v-show="show.box7" :src="boxes.box7" alt=" "/>
				</div>
				<div class="move-box" id="box-8" v-on:click="makeMove(8)">
					<img v-show="show.box8" :src="boxes.box8" alt=" "/>
				</div>
			</div>
		</div>
  </div>
</template>

<script>
export default {
  name: "board",
  props: {
    position: Array,
		turn: String,
		playable: Boolean,
		/*
			"o" - o's turn
			"x" - x's turn
		*/
  },
	data() {
		return {
			gameover: false,
			boxes: {
				box0: "#",
				box1: "#",
				box2: "#",
				box3: "#",
				box4: "#",
				box5: "#",
				box6: "#",
				box7: "#",
				box8: "#",
			},

			show: {
				box0: false,
				box1: false,
				box2: false,
				box3: false,
				box4: false,
				box5: false,
				box6: false,
				box7: false,
				box8: false,
			},

		}
	},
	computed: {

	},
	methods: {
		checkForFinish() {
			// First check for an actual win
			let p = this.position;
			function checker(p1, p2, p3) {
	 			if ((p1 == 'x') && (p2 == 'x') && (p3 == 'x')) {
					return "x-won";
				}
				else if ((p1 == 'o') && (p2 == 'o') && (p3 == 'o')) {
					return "o-won";
				}
				else {
					return false;
				}
			}
			let wins = [
				checker(p[0][0], p[0][1], p[0][2]),
				checker(p[1][0], p[1][1], p[1][2]),
				checker(p[2][0], p[2][1], p[2][2]),
				checker(p[0][0], p[1][0], p[2][0]),
				checker(p[0][1], p[1][1], p[2][1]),
				checker(p[0][2], p[1][2], p[2][2]),
				checker(p[0][0], p[1][1], p[2][2]),
				checker(p[0][2], p[1][1], p[2][0])];
			for (const result of wins) {
				if (result) {
					return result;
				}
			}

			if ((p[0][0] != '-') &&
					(p[0][1] != '-') &&
					(p[0][2] != '-') &&
					(p[1][0] != '-') &&
					(p[1][1] != '-') &&
					(p[1][2] != '-') &&
					(p[2][0] != '-') &&
					(p[2][1] != '-') &&
					(p[2][2] != '-')) {
				return "t"
			} else {
				return false;
			}
		},

		makeMove(move) {
			if (this.gameover || !this.playable) 
				return
			let row = Math.floor(move / 3);
			let col = move % 3;
			if (this.position[row][col] != "-") {
				return;
			} else {
				this.position[row][col] = this.turn;
			}
			switch(this.turn) {
				case "x":
					this.boxes["box" + move] = require("@/assets/x.png");
					this.turn = "o";
					this.show["box" + move] = true;
					break;
				case "o": 
					this.boxes["box" + move] = require("@/assets/o.jpg");
					this.turn = "x";
					this.show["box" + move] = true;
					break;
				default:
					break;
			}
			this.gameover = this.checkForFinish();
			if (this.gameover) {
				this.$emit("gameover", this.gameover);
			}
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.board {
	display:flex;
	flex-direction:column;
	justify-content:center;
	align-items:center;
}
#container{
	display:flex;
	flex-direction:column;
	flex-wrap:wrap;
	width:90vw;
	height:90vw;
	justify-content:center;
	align-items:center;
	margin:0 0;
}
.row {
	display:flex;
	flex-direction:row;
	height:30vw;
	width:100%;
}
.move-box {
	display:flex;
	justify-content:center;
	align-items:center;
	flex-grow:1;
	flex-basis:0;
	margin:0 0;
}
.move-box img {
	width:70%;
	height:70%;
	object-fit:contain;
}
#box-0 {
	border-right:1px solid black;
	border-bottom:1px solid black;
}
#box-1 {
	border-left:1px solid black;
	border-right:1px solid black;
	border-bottom:1px solid black;
}
#box-2 {
	border-left:1px solid black;
	border-bottom:1px solid black;
}
#box-3 {
	border-right:1px solid black;
	border-top:1px solid black;
	border-bottom:1px solid black;
}
#box-4 {
	border-right:1px solid black;
	border-left:1px solid black;
	border-top:1px solid black;
	border-bottom:1px solid black;
}
#box-5 {
	border-left:1px solid black;
	border-top:1px solid black;
	border-bottom:1px solid black;
}
#box-6 {
	border-right:1px solid black;
	border-top:1px solid black;
}
#box-7 {
	border-right:1px solid black;
	border-left:1px solid black;
	border-top:1px solid black;
}
#box-8 {
	border-top:1px solid black;
	border-left:1px solid black;
}

</style>
