<template>
  <div id="app">
		<div id="header">
			<h1>Tic-Tac-Toe</h1>
		</div>
		<div id="nav">
      <router-link to="/play">Play</router-link> |
      <router-link to="/leaderboard">Leaderboard</router-link>
    </div>
    <router-view />
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
</style>
