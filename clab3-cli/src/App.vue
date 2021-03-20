<template>
  <div id="app">
		<div id="page">
			<div id="header">
				<h1>Tic-Tac-Toe</h1>
			</div>
			<div id="nav">
				<router-link to="/play">Play</router-link> |
				<router-link to="/leaderboard">Leaderboard</router-link>
			</div>
			<router-view />
			<div id="footer">
				<a href="https://github.com/issmith962/cs260-clab3.git">https://github.com/issmith962/cs260-clab3.git</a>
			</div>
		</div>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#page {
	display:flex;
	flex-direction:column;
}

#nav {
  padding: 30px;
	padding-top: 10px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}

#footer {
	margin-top:auto;
	display:flex;
	justify-content:center;
	align-items:center;
	width:100%;
	padding:5px;
	
	position:fixed;
	bottom:0;
}

</style>
