<template>
  <div class="play">
		<div id="player-names">
			<form onsubmit="event.preventDefault();">
				<label for="xNameInput">Player X Name:</label>
				<input type="text" id="xNameInput" v-model="xName" name="xNameInput" maxlength="4">
			</form>
			<form onsubmit="event.preventDefault();">
				<label for="oNameInput">Player O Name:</label>
				<input type="text" id="oNameInput" v-model="oName" name="oNameInput" maxlength="4">
			</form>
		</div>
    <board @gameover="onGameover" :turn="turn" :position="position" :gameover="gameover" :playable="validNames"/>
			
		<button v-if="gameover" id='play-again' v-on:click="playAgain()">Play Again!</button>
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
		}
			 	
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

#player-names {
	display:flex;
	flex-direction:row;
	justify-content:center;
}

</style>
