<template>
	<div class="container">
		<div class="product-info-container">
			<div class="product-info">
				<div class="product-wrapper">
					<div class="menu">
						<ul>
							<li @mouseenter="currentindex=1" class="one">
								<a :class="{'selected' : currentindex === 1}" ref="one" href="#">Beschrijving</a>
							</li>
							<li @mouseenter="currentindex=2" class="two">
								<a :class="{'selected' : currentindex === 2}" ref="two" href="#">Fitting</a>
							</li>
							<li @mouseenter="currentindex=3" class="three">
								<a :class="{'selected' : currentindex === 3}" ref="three" href="#">Levering</a>
							</li>
							<li @mouseenter="currentindex=4" class="four">
								<a :class="{'selected' : currentindex === 4}" ref="four" href="#">Jouw Mening</a>
							</li>
							<hr :style="{ margin: computedMargin, width: computedWidth + 'px'}" />
						</ul>
					</div>
					<div class="text-wrapper">
						<transition name="slide">
							<div v-if="currentindex == 1" class="beschrijving">
								<div class="material-wrapper">
									<p>MATERIAAL & WASVOORSCHRIFT</p>
									<p>Materiaal buitenlaag:</p>
									<p>Materiaalverwerking:</p>
									<p>Wasvoorschrift:</p>
								</div>
								<div class="over-the-product-wrapper">
									<p>ALLES OVER DIT PRODUCT</p>
									<p>Halslijn / kraag:</p>
									<p>Patroon:</p>
									<p>Artikelnummer:</p>
								</div>
								<div class="author-wrapper">
									<p>CARIN WESTER</p>
								</div>
							</div>
						</transition>
						<transition name="slide">
							<div v-if="currentindex == 2" class="fitting">
								<p>Lichaamslengte model:</p>
								<p>Lengte:</p>
								<p>Mouwlengte:</p>
								<p>Mouwlengte:</p>
								<p>Totale lengte:</p>
							</div>
						</transition>
						<transition name="slide">
							<div v-if="currentindex == 3" class="levering">
								<p>Gratis verzending en retour</p>
								<p>100 dagen recht op retour</p>
							</div>
						</transition>
						<transition name="slide">
							<div v-if="currentindex == 4" class="mening">
								<p>Dit artikel heeft nog geen beoordelingen. Wil jij de eerste zijn?</p>
								<button class="mening-button">
									<div class="button-text-container">
										<span>DEEL JOUW ERVARING</span>
									</div>
								</button>
							</div>
						</transition>
					</div>
				</div>
			</div>
			<div class="product-image">
				<div class="image-container"></div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	data() {
		return {
			currentindex: 1,
			width: 0,
			isMounted: false
		};
	},
	methods: {
		getElementWidth(ref) {
			return "" + this.$refs[ref].clientWidth;
		}
	},
	computed: {
		computedMargin() {
			if (this.currentindex == 2) return "0 0 0 calc(25% + 30px)";
			else if (this.currentindex == 3) return "0 0 0 calc(50% + 23.08px)";
			else if (this.currentindex == 4) return "0 0 0 calc(75% + 10.08px)";
			return "0 0 0 8px";
		},
		computedWidth() {
			if (this.isMounted) {
				if (this.currentindex == 2) return this.getElementWidth("two");
				else if (this.currentindex == 3)
					return this.getElementWidth("three");
				else if (this.currentindex == 4)
					return this.getElementWidth("four");
				return this.getElementWidth("one");
			}
			return null;
		}
	},
	mounted() {
		this.isMounted = true;
	}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.beschrijving,
.fitting,
.levering,
.mening {
	position: absolute;
	top: 0;
	left: 0;
}
.text-wrapper {
	position: relative;
	min-width: 100px;
	min-height: 100px;
}
.slide-leave-active,
.slide-enter-active {
	transition: 0.7s;
}
.slide-enter {
	transform: translate(200%, 0);
}
.slide-leave-to {
	transform: translate(-300%, 0);
}
.button-text-container {
	display: flex;
	align-items: center;
	justify-content: center;
}
.button-text-container > span {
	color: white;
}
.mening-button {
	border-width: 2px;
	border-radius: 2px;
	background-color: #ff6900;
	border-color: #ff6900;
	outline: transparent;
	height: 46px;
	width: 50%;
	min-width: 80px;
}
.text-wrapper {
	margin-top: 24px;
	overflow: hidden;
}
.text-wrapper p {
	margin: 0;
	text-align: start;
	font-size: 12px;
	font-weight: 700;
}
.product-wrapper {
	height: 100%;
	margin-left: 15%;
	padding-top: 24px;
}
.selected {
	color: #1a1a1a;
}
* {
	box-sizing: border-box;
}
.product-info-container {
	max-width: 100%;
	max-height: 600px;
	background: rgb(243, 243, 243);
	display: flex;
}
.product-info {
	flex: 1;
}
.product-image {
	flex: 1;
}
.image-container {
	max-height: 870px;
	height: 600px;
	width: 100%;
	background-repeat: no-repeat;
	background-position: center top;
	background-image: url("https://mosaic01.ztat.net/vgs/static/pdp_review_3.jpg");
}
.container {
	max-width: 1200px;
	margin: 0 auto;
}
ul {
	width: 430px;
	padding: 0;
	margin: 0;
}
ul li {
	display: inline-block;
	text-align: center;
	width: 25%;
}
a {
	text-transform: uppercase;
	font-size: 12px;
	display: inline-block;

	text-decoration: none;
	color: #999;
	font-weight: bold;
}
hr {
	height: 3px;

	background: #ff6900;
	border: none;
	transition: all 0.4s ease;
}
</style>
