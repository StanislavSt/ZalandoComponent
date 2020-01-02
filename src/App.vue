<template>
	<div id="app">
		<ZalandoMenu :menuItems="menuItems" :images="images" :rawHtml="rawHtml" />
	</div>
</template>

<script>
import ZalandoMenu from "./components/ZalandoMenu.vue";

export default {
	name: "app",
	data() {
		return {
			menuItems: ["beschrijving", "fitting", "together", "WITHMEISYOU"],
			images: [
				"https://img02.ztat.net/article/RO/54/1E/03/GN/11/RO541E03G-N11@12.jpg?impolicy=detail",
				"https://img01.ztat.net/article/RO/54/1E/03/KQ/11/RO541E03K-Q11@9.jpg?impolicy=detail",
				"https://img01.ztat.net/article/RO/54/1E/03/KE/11/RO541E03K-E11@9.jpg?impolicy=detail",
				"https://mosaic01.ztat.net/vgs/static/pdp_review_3.jpg"
			],
			rawHtml: [
				`		<p>MATERIAAL & WASVOORSCHRIFT</p>
						<p>Materiaal buitenlaag:</p>
						<p>Materiaalverwerking:</p>
						<p>Wasvoorschrift:</p>`,
				`				<p>Lichaamslengte model:</p>
								<p>Lengte:</p>
								<p>Mouwlengte:</p>
								<p>Mouwlengte:</p>
								<p>Totale lengte:</p>`,
				`								<p>Gratis verzending en retour</p>
												<p>100 dagen recht op retour</p>`,
				`				<p>Dit artikel heeft nog geen beoordelingen. Wil jij de eerste zijn?</p>
								<button class="mening-button">
									<div class="button-text-container">
										<span>DEEL JOUW ERVARING</span>
									</div>
								</button>`
			]
		};
	},
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
