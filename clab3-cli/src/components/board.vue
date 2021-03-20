<template>
  <div class="board">
		<div id="container">
			<div class="row">
				<div class="move-box" id="box-1">
					<img class="x-img" src="@/assets/x.png"/>
				</div>
				<div class="move-box" id="box-2">
					<img class="x-img" src="@/assets/x.png"/>
				</div>
				<div class="move-box" id="box-3">
					<img class="x-img" src="@/assets/x.png"/>
				</div>
			</div>
			<div class="row">
				<div class="move-box" id="box-4">
					<img class="x-img" src="@/assets/x.png"/>
				</div>
				<div class="move-box" id="box-5">
					<img class="o-img" src="@/assets/o.jpg"/>
				</div>
				<div class="move-box" id="box-6"></div>
			</div>
			<div class="row">
				<div class="move-box" id="box-7"></div>
				<div class="move-box" id="box-8"></div>
				<div class="move-box" id="box-9">
					<img class="o-img" src="@/assets/o.jpg"/>
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
		/*
			"o" - o's turn
			"x" - x's turn
			"o-won" - o's won
			"x-won" - x's won
		*/
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.board {
	display:flex;
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
.x-img {
	width:60%;
	height:60%;
	object-fit:contain;
}
.o-img {
	width:70%;
	height:70%;
	object-fit:contain;
}
#box-1 {
	border-right:1px solid black;	
	border-bottom:1px solid black;	
}
#box-2 {
	border-left:1px solid black;	
	border-right:1px solid black;	
	border-bottom:1px solid black;	
}
#box-3 {
	border-left:1px solid black;	
	border-bottom:1px solid black;	
}
#box-4 {
	border-right:1px solid black;	
	border-top:1px solid black;	
	border-bottom:1px solid black;	
}
#box-5 {
	border-right:1px solid black;	
	border-left:1px solid black;	
	border-top:1px solid black;	
	border-bottom:1px solid black;	
}
#box-6 {
	border-left:1px solid black;	
	border-top:1px solid black;	
	border-bottom:1px solid black;	
}
#box-7 {
	border-right:1px solid black;	
	border-top:1px solid black;	
}
#box-8 {
	border-right:1px solid black;	
	border-left:1px solid black;	
	border-top:1px solid black;	
}
#box-9 {
	border-top:1px solid black;	
	border-left:1px solid black;	
}

</style>
