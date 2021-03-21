<template>
  <div class="play">
		<div id="player-names">
			<form onsubmit="event.preventDefault();">
				<label for="xNameInput">Player X Name:</label>
				<input type="text" id="xNameInput" v-model="xName" name="xNameInput" maxlength="4">
			</form>
			<form onsubmit="event.preventDefault();">
				<label for="oNameInput">Player O Name:</label>
				<input type="text" id="oNameInput" v-model="yName" name="oNameInput" maxlength="4">
			</form>
		</div>
    <board @gameover="onGameover" :turn="turn" :position="position" :playable="validNames"/>
			
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
			yName: "",
			turn: "x", 
			position: [['-', '-', '-'], 
								['-', '-', '-'], 
								['-', '-', '-']],
		}
	},
	methods: {
		onGameover(gameover) {
			this.gameover = gameover; 
		}, 
		playAgain() {
			this.gameover = false;
			this.turn = "x"; 
			this.position = [['-', '-', '-'], ['-', '-', '-'], ['-', '-', '-']]; 
		}
			 	
	},
	computed: {
		validNames() {
			return (this.xName != this.yName) 
				&& !(/\s/g.test(this.xName)) 
				&&  !(/\s/g.test(this.yName))
				&& (this.xName != "")
				&& (this.yName != ""); 
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
