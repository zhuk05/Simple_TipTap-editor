<template>
	<div class="view">
		<div id="editors">
			<tip-tap />
		</div>
	</div>
</template>

<script setup>
import TipTap from './components/TipTap.vue'
</script>

<style>
#app {
	font-family: Avenir, Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
	margin-left: 20px;
}

body {
	overflow-x: hidden;
	margin: 0 20px;
}

* {
	box-sizing: border-box;
}

body,
#app {
	height: 100vh;
	padding: 0;
	margin: 0;
}

.view {
	display: flex;
	flex-direction: column;
	height: inherit;
}

#editors {
	flex-grow: 1;
}

.header {
	display: flex;
	gap: 20px;
	padding: 5px 20px;
	background-color: white;
  width: 100%;
}

.header .button.is-active {
	background: lightsalmon;
}

.button {
	border: none;
	padding: 12px 20px;
	border-radius: 5px;
}
</style>
