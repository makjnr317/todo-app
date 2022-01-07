<template>
	<h1>#todo</h1>
	<Main/>
</template>

<script>
import Main from "./components/Main.vue"

export default {
  name: 'App',
  components: { Main }
}
</script>

<style>
#app{
	padding-top:32px;
}

h1{
	font-family: Raleway;
	font-weight: bold;
	letter-spacing: -0.045em;
	font-size: 36px;
	color: #333333;
	text-align: center;
	margin-bottom: 58px;
}
</style>
