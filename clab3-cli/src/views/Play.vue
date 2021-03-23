<template>
  <div class="play">
		<div id="player-names">
			<form id="x-name-form" onsubmit="event.preventDefault();">
				<label for="x-name-input">Player X Name:</label>
				<br>
				<input type="text" id="x-name-input" v-model="xName" name="xNameInput" maxlength="4">
			</form>
			<form  id="o-name-form" onsubmit="event.preventDefault();">
				<label for="o-name-input">Player O Name:</label>
				<br>
				<input type="text" id="o-name-input" v-model="oName" name="oNameInput" maxlength="4">
			</form>
		</div>
    <board id="board" @gameover="onGameover" :position="position" :gameover="gameover" :playable="validNames"/>
		<div id="name-alert" v-if="!validNames">
			<h3 id="name-alert-text">Make sure both players have names (4 char. max)</h3>
		</div>
			
		<div id="button-container">
			<button v-if="gameover" id='play-again' v-on:click="playAgain()">Play Again!</button>
			<button v-if="gameover" id='clear' v-on:click="clear()">Clear</button>
		</div>
  </div>
</template>

<script>
// @ is an alias to /src
import board from "@/components/board.vue";

export default {
  name: "Play",
  components: {
    board,
  },
	data() {
		return {
			gameover: false,
			xName: "", 
			oName: "",
			position: [['-', '-', '-'], 
								['-', '-', '-'], 
								['-', '-', '-']],
		}
	},
	methods: {
		onGameover(gameover) {
			this.gameover = gameover; 
			this.logGame(); 
		}, 
		logGame() {
			let records = this.$root.$data.playerRecords;
			// example record: {name: asdf, wins: 10, losses: 15, ties: 100} 
			let xRecord = records.find(el => el.name == this.xName); 
			let oRecord = records.find(el => el.name == this.oName); 
			if (xRecord == undefined) {
				xRecord = {name: this.xName, wins: 0, losses: 0, ties: 0}; 
				records.push(xRecord); 
			}
			if (oRecord == undefined) {
				oRecord = {name: this.oName, wins: 0, losses: 0, ties: 0}; 
				records.push(oRecord); 
			}
				
			if (this.gameover == "x-won") {
				xRecord.wins++;
				oRecord.losses++; 
			} else if (this.gameover == "o-won") {
				xRecord.losses++;
				oRecord.wins++;
			} else if (this.gameover == "t") {
				xRecord.ties++; 
				oRecord.ties++;
			} else {
				console.log("ERROR with gameover code");
			}
		},
		playAgain() {
			this.gameover = false;
			this.position = [['-', '-', '-'], ['-', '-', '-'], ['-', '-', '-']]; 
		},
		clear() {
			this.gameover = false;
			this.position = [['-', '-', '-'], ['-', '-', '-'], ['-', '-', '-']]; 
			this.xName = ""; 
			this.oName = ""; 
		},
			 	
	},
	computed: {
		validNames() {
			return (this.xName != this.oName) 
				&& !(/\s/g.test(this.xName)) 
				&&  !(/\s/g.test(this.oName))
				&& (this.xName != "")
				&& (this.oName != ""); 
		},
	}, 
};
</script>

<style scoped>
.play {
	display: flex; 
	flex-direction: column; 
}
#player-names {
	display:flex;
	flex-direction:row;
	justify-content:center;
	margin-bottom:10px;
}
#x-name-form {
	margin-right:20px;
}
#o-name-form {
	margin-left:20px;
}
#x-name-input {
	width:100px;
}
#o-name-input {
	width:100px;
}
#name-alert {
	display:flex; 
	justify-content:center;
}
#name-alert-text {
	padding: 0px 50px; 
}
#board {
	margin-top:10px;
	margin-bottom:10px;
}
#button-container {
	display:flex;
	flex-direction:column;
	align-items:center;
	margin-bottom:20px;
}
#play-again {
	width:50%;
	border:1px solid black;
	margin-bottom:5px;
	padding:4px;
}
#clear {
	width:50%;
	border:1px solid black;
	padding:4px;
}

@media (min-width: 700px) {
	#board {
	}
}

</style>
