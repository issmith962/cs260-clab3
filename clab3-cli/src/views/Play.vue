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
    <board turn="x" :position=
			"[ 
				['-', '-', '-'], 
				['-', '-', '-'], 
				['-', '-', '-']
			]" />
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
			xName: "", 
			yName: "",
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
