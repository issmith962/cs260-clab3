<template>
  <div class="leaderboard">
		<button v-on:click="toggleEdit">{{editMessage}}</button>
		<div id="ranking-grid">
			<div class="row" id="column-headers">
				<div class="headers">
					<p>Rank</p>
				</div>	
				<div class="headers">
					<p>Name</p>
				</div>	
				<div class="headers">
					<p>Wins</p>
				</div>	
				<div class="headers">
					<p>Losses</p>
				</div>	
				<div class="headers">
					<p>Ties</p>
				</div>	
				<div class="headers">
					<p>Delete</p>
				</div>	
			</div>
			<div class="row" id="rankings" v-for="(record, index) in records" :key="record.id">
				<div class="rank">
					<p>{{"#" + (index + 1)}}</p>
				</div>	
				<div class="name">
					<input v-if="editEnabled" type="text" maxlength="4" :name="'newName'+record.id" v-model="records[index].name"> 
					<p v-else>{{record.name}}</p>
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
			editEnabled: false,
			editMessage: "Edit Player Names",
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
		toggleEdit() {
			if (this.editEnabled) {
				this.$root.$data.playerRecords = this.records.slice(0);
				this.editMessage = "Edit Player Names";
			} else {
				this.editMessage = "Save player name changes";
			}
			this.editEnabled = !this.editEnabled;
		},
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
.leaderboard {
	display:flex;
	flex-direction:column;
}
input {
	width:50%;
	}
#ranking-grid {
	display: flex; 
	flex-direction: column; 
	margin: 10px 5px; 
}
#column-headers {
	background-color: #b50717;
	color:#131313;
	font-weight:bold;
	padding: 0px 5px;
}
.headers {
	flex-basis:0; 
	flex-grow:1;
	display:flex;
	justify-content:center;
	align-items:center;
}
#rankings {
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
@media (min-width: 700px) {
	.leaderboard {
		display:flex;
		justify-content:center;
		align-items:center;
	}
	#ranking-grid {
		width:60%;
		border:5px solid #b50717;
	}

}
</style>
