<template>
	<div class="container">
		<div class="product-info-wrapper">
			<div class="product-info">
				<div class="menu">
					<ul>
						<div v-for="(item,index) in menuItems" :key="index" class="list-item">
							<li @mouseenter="changeIndex(index+1)">
								<a :class="{'selected' : currentindex === index+1}" :ref="'element' + (index+1)">{{item}}</a>
							</li>
						</div>
					</ul>
					<hr :style="{ margin: computedMargin, width: computedWidth +'px'}" />
				</div>
				<div class="text-wrapper">
					<transition v-for="(item,index) in rawHtml" :key="index" :name="computedTransition">
						<div v-if="currentindex === index +1" class="beschrijving">
							<span v-html="item"></span>
						</div>
					</transition>
				</div>
			</div>
		</div>
		<div class="product-image-wrapper">
			<div class="product-image" :style="{ backgroundImage: 'url(' + computedImageUrl + ')' }"></div>
		</div>
	</div>
</template>

<script>
export default {
	props: ["menuItems", "images", "rawHtml"],
	data() {
		return {
			isMounted: false,
			currentindex: 1,
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
				this.slideDirection = "left";
				this.interval = setInterval(() => {
					this.currentindex++;
					if (this.currentindex === index) {
						clearInterval(this.interval);
					}
				}, 20);
			}
			if (index < this.currentindex) {
				this.slideDirection = "right";
				this.interval = setInterval(() => {
					this.currentindex--;
					if (this.currentindex === index) {
						clearInterval(this.interval);
					}
				}, 20);
			}
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
					(this.currentindex - 1) * 26 + //This is if we assume margin-right:26px
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
			if (this.slideDirection === "left") return "slide-left";
			else return "slide-right";
		},
		computedImageUrl() {
			if (this.images.length >= this.currentindex)
				return this.images[this.currentindex - 1];
			else return this.images[0];
		}
	},
	mounted() {
		this.isMounted = true;
	}
};
</script>

<style scoped>
* {
	box-sizing: border-box;
}
.container {
	max-width: 1200px;
	height: 600px;
	margin: 0 auto;
	background: rgb(243, 243, 243);
	display: flex;
}
.text-wrapper {
	position: relative;
	margin-top: 24px;
	overflow: hidden;
	width: 100%;
	height: 100%;
}
.product-info {
	height: 100%;
	margin-left: 15%;
	padding-top: 24px;
}
.beschrijving {
	position: absolute;
	top: 0;
	left: 0;
}
.product-info-wrapper,
.product-image-wrapper {
	flex: 1;
}
.product-image {
	height: 100%;
	width: 100%;
}
.cluster-divider {
	display: none;
}
/*Menu */
ul {
	max-width: 500px;
	padding: 0;
	margin: 0;
	display: flex;
	align-items: flex-start;
}
ul li {
	list-style: none;
	margin-right: 26px;
}
ul li a {
	text-transform: uppercase;
	font-size: 12px;
	display: inline-block;
	color: #999;
	font-weight: bold;
	cursor: pointer;
}
.selected {
	color: #1a1a1a;
}
hr {
	height: 3px;
	background: #ff6900;
	border: none;
	transition: all 0.4s ease;
}
/* Transition */
.slide-left-leave-active,
.slide-left-enter-active,
.slide-right-leave-active,
.slide-right-enter-active {
	transition: 0.4s;
}
.slide-left-enter {
	transform: translate(200%, 0);
}
.slide-left-leave-to {
	transform: translate(-350%, 0);
}
.slide-right-enter {
	transform: translate(-200%, 0);
}
.slide-right-leave-to {
	transform: translate(350%, 0);
}
@media screen and (max-width: 920px) {
	.product-info {
		margin-left: 5%;
	}
}
@media screen and (max-width: 800px) {
	.slide-left-leave-active,
	.slide-left-enter-active,
	.slide-right-leave-active,
	.slide-right-enter-active {
		transition: 0;
	}
	.slide-left-enter,
	.slide-left-leave-to,
	.slide-right-enter,
	.slide-right-leave-to {
		transform: none;
	}
	.list-item {
		height: 100%;
		width: 100%;
		border-bottom: solid 1px #ddd;
		display: flex;
	}
	.container {
		display: block;
		height: 300px;
		width: 100%;
	}
	.product-info-wrapper {
		width: 100%;
		height: 100%;
	}
	.product-image {
		display: none;
	}
	.product-info {
		padding: 0;
		margin: 0;
		width: 100%;
	}
	hr {
		display: none;
	}
	ul {
		height: 100%;
		max-width: 800px;
		flex-direction: column;
		justify-content: space-between;
	}
	ul li {
		margin: auto 0;
		width: 100%;
	}
	ul li a {
		color: black;
		margin-left: 1rem;
	}
	.menu {
		height: 100%;
	}
	.text-wrapper {
		display: none;
	}
}
</style>
