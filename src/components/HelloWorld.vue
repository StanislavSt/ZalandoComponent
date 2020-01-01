<template>
	<div class="container">
		<div class="product-info-container">
			<div class="product-info">
				<div class="product-wrapper">
					<div class="menu">
						<ul>
							<li v-for="(item,index) in menuItems" :key="index" @mouseenter="changeIndex(index+1)">
								<a :class="{'selected' : currentindex === index+1}" :ref="'element' + (index+1)">{{item}}</a>
							</li>
						</ul>
						<hr :style="{ margin: computedMargin, width: computedWidth +'px'}" />
					</div>
					<div class="text-wrapper">
						<transition :name="computedTransition">
							<div v-if="currentindex == 1" class="beschrijving">
								<p>MATERIAAL & WASVOORSCHRIFT</p>
								<p>Materiaal buitenlaag:</p>
								<p>Materiaalverwerking:</p>
								<p>Wasvoorschrift:</p>
							</div>
						</transition>
						<transition :name="computedTransition">
							<div v-if="currentindex == 2" class="fitting">
								<p>Lichaamslengte model:</p>
								<p>Lengte:</p>
								<p>Mouwlengte:</p>
								<p>Mouwlengte:</p>
								<p>Totale lengte:</p>
							</div>
						</transition>
						<transition :name="computedTransition">
							<div v-if="currentindex == 3" class="levering">
								<p>Gratis verzending en retour</p>
								<p>100 dagen recht op retour</p>
							</div>
						</transition>
						<transition :name="computedTransition">
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
			previousindex: 1,
			isMounted: false,
			menuItems: ["beschrijving", "fitting", "together", "WITHMEISYOU"],
			images: [],
			slideDirection: "left"
		};
	},
	methods: {
		getElementWidth(index) {
			return this.$refs["element" + index][0].clientWidth;
		},
		getAllElementsWidth(numberOfElements) {
			let i = 1;
			let width = 0;
			while (i <= numberOfElements) {
				width += this.getElementWidth(i);
				i++;
			}
			return width;
		},
		changeIndex(index) {
			clearInterval(this.interval);
			if (index > this.currentindex) {
				this.previousindex = this.currentindex;
				this.slideDirection = "left";
				this.interval = setInterval(() => {
					this.currentindex++;
					if (this.currentindex === index) {
						clearInterval(this.interval);
					}
				}, 20);
			}
			if (index < this.currentindex) {
				this.previousindex = this.currentindex;
				this.slideDirection = "right";
				this.interval = setInterval(() => {
					this.currentindex--;
					if (this.currentindex === index) {
						clearInterval(this.interval);
					}
				}, 20);
			}
		},
		assignSlide(x) {
			this.lastSlide = x;
		}
	},
	computed: {
		computedMargin() {
			if (this.currentindex > 1) {
				return (
					"0 0 0 " +
					"calc(" +
					this.getAllElementsWidth(this.currentindex - 1) +
					"px + " +
					(this.currentindex - 1) * 26 +
					"px"
				);
			}
			return "0 0 0 0";
		},
		computedWidth() {
			if (this.isMounted) {
				return this.getElementWidth(this.currentindex);
			}
			return null;
		},
		computedTransition() {
			if (this.slideDirection == "left") return "slide-left";
			else return "slide-right";
		}
	},
	mounted() {
		this.isMounted = true;
	}
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
* {
	box-sizing: border-box;
}
.container {
	max-width: 1200px;
	margin: 0 auto;
}
ul {
	max-width: 500px;
	padding: 0;
	margin: 0;
	display: flex;
}
ul li {
	list-style: none;
	text-align: center;
	margin-right: 26px;
	align-self: flex-start;
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

.selected {
	color: #1a1a1a;
}
.slide-left-leave-active,
.slide-left-enter-active,
.slide-right-leave-active,
.slide-right-enter-active {
	transition: 0.4s;
}
.slide-left-enter {
	transform: translate(200%, 0);
}
.slide-right-enter {
	transform: translate(-200%, 0);
}
.slide-left-leave-to {
	transform: translate(-300%, 0);
}
.slide-right-leave-to {
	transform: translate(300%, 0);
}
/*  */
/*  */
/*  */
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
	position: relative;
	min-width: 100px;
	min-height: 100px;
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
.beschrijving,
.fitting,
.levering,
.mening {
	position: absolute;
	top: 0;
	left: 0;
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
</style>
