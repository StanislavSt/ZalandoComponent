<template>
	<div id="app">
		<ZalandoMenu />
	</div>
</template>

<script>
import ZalandoMenu from "./components/ZalandoMenu.vue";

export default {
	name: "app",
	components: {
		ZalandoMenu
	}
};
</script>

<style>
#app {
	font-family: "Avenir", Helvetica, Arial, sans-serif;
	-webkit-font-smoothing: antialiased;
	-moz-osx-font-smoothing: grayscale;
	color: #2c3e50;
}
</style>
