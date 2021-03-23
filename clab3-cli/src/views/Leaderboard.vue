<template>
  <div class="leaderboard">
		<div id="ranking-grid">
			<div class="row" id="column-headers">
				<div>
					<p>Rank</p>
				</div>	
				<div>
					<p>Name</p>
				</div>	
				<div>
					<p>Wins</p>
				</div>	
				<div>
					<p>Losses</p>
				</div>	
				<div>
					<p>Ties</p>
				</div>	
				<div>
					<p>Delete?</p>
				</div>	
			</div>
			<div class="row" id="rankings" v-for="(record, index) in records" :key="record.id">
				<div class="rank">
					<p>{{"#" + (index + 1)}}</p>
				</div>	
				<div class="name">
					<p>{{record.name}}</p>
				</div>	
				<div class="wins">
					<p>{{record.wins}}</p>
				</div>	
				<div class="losses">
					<p>{{record.losses}}</p>
				</div>	
				<div class="ties">
					<p>{{record.ties}}</p>
				</div>	
				<div class="delete">
					<button v-on:click="deleteRecord(record)">X</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "Leaderboard",
	data() {
		return {
		}
	},
	computed: {
		records: function () {
			let playerRecords = Array.from(this.$root.$data.playerRecords);  
			return playerRecords.sort(function (a, b) {
				let winsA = a.wins; 
				let winsB = b.wins;
				if (winsA < winsB) return -1; 
				if (winsA > winsB) return 1; 

				let lossesA = a.losses; 
				let lossesB = b.losses;
				if (lossesA > lossesB) return -1; 
				if (lossesA < lossesB) return 1; 

				let tiesA = a.ties; 
				let tiesB = b.ties;
				if (tiesA < tiesB) return -1; 
				if (tiesA > tiesB) return 1; 

				return 0; 
			}).reverse(); 
		},
	},
	methods: {
		deleteRecord(record) {
			for (let i = 0; i < this.$root.$data.playerRecords.length; i++) {
				if (record === this.$root.$data.playerRecords[i]) {
					this.$root.$data.playerRecords.splice(i, 1); 
					break;
				}
			}
		},
	},
};
</script>

<style scoped>
#ranking-grid {
	display: flex; 
	flex-direction: column; 
	margin-bottom:10px;
}
#column-headers {
	background-color: #b50717;
	color:#131313;
	font-weight:bold;
	padding: 0px 5px;
}
#rankings {
	padding: 0px 5px;
}
.row {
	display:flex;
	flex-direction: row; 
	justify-content:space-between; 
}
.rank {
	background-color:#bfbfbf;
	flex-basis:0; 
	flex-grow:1; 
}
.name {
	flex-basis:0; 
	flex-grow:1; 
}
.wins {
	background-color:#bfbfbf;
	flex-basis:0; 
	flex-grow:1; 
}
.losses {
	flex-basis:0; 
	flex-grow:1; 
}
.ties {
	background-color:#bfbfbf;
	flex-basis:0; 
	flex-grow:1; 
}
.delete {
	flex-basis:0; 
	flex-grow:1; 
	display:flex;
	justify-content:center; 
	align-items:center;
}
</style>
