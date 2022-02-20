<template>
	<Carousel :itemsToShow="1.1" :wrapAround="false">
		<Slide v-for="(card, index) in card_lists" :key="index">
			<div class="carousel__item"  >
						<div class="card p-1" id="show-card-no"  :class="card.isFrozen">	
				 			<span><img :src="eye_icon" alt="eye_icon"> Show card number</span>
						</div>
				<div class="card card--styles"  :class="card.isFrozen"  id="debit-card" style="">
				
					<p>
						<img
						v-if="card.isFrozen=='frozen'"
							id="frozen-logo"
							:src="frozen_icon"
							alt="logo_white"
						/>
						<img
							id="card__aspire-logo--style"
							:src="logo_white"
							alt="logo_white"
						/>
					</p>
					<h5 class="card__h3--style ps-3">
						{{ card.name }}
					</h5>
					<div class="card-body card-body--styles" >
						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>

						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>

						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>
						<span class="dot"></span>

						<span class="ps-1">2</span>
						<span class="ps-1">0</span>
						<span class="ps-1">2</span>
						<span class="ps-1">0</span>
					</div>
					<div
						class="row mx-2 align-items-center"
						style="font-size: 0.8rem; font-weight: bold"
					>
						<div class="col">Thru:{{ card.exp_date }}</div>

						<div class="col" style="position: relative; right: 3rem">
							CVV:
							<span style="font-size: 1rem; position: relative; top: 3px"
								>***</span
							>
						</div>
					</div>
					<p>
						<img
							style="
								float: right;
								padding-bottom: 0.5rem;
								padding-right: 1.5rem;
							"
							:src="visa_logo"
							alt="visa_logo"
						/>
					</p>
				</div>
			</div>
		</Slide>
		<template ref="temp" #addons>
			<Pagination />
		</template>
	</Carousel>
</template>

<script>
import { defineComponent } from "vue";
import { Carousel, Pagination, Slide } from "vue3-carousel";

import "vue3-carousel/dist/carousel.css";

export default defineComponent({
	name: "Autoplay",
	components: {
		Carousel,
		Slide,
		Pagination,
	},
	props: {
		card_lists: Array,
	},

	data() {
		return {
			data: null,
			visa_logo: require("../assets/asset/Visa Logo.svg"),
			logo_white: require("../assets/asset/Logo-2.svg"),
			frozen_icon:require("../assets/asset/nature (1).svg"),
			eye_icon:require("../assets/asset/remove_red_eye-24px.svg")
		};
	},
});
</script>

<style scoped>
#debit-card {
	position: relative;
	border-radius: 1rem;
	height: 100%;
	margin: 1rem auto;
}
.card__h3--style {
	font-weight: bold;
}
#frozen-logo{
	position: relative;
	top:0.5rem;
	left: 0.8rem;
	height:20px;
	width: 20px;
	float: left;
	background: inherit;
}

#card__aspire-logo--style {
	position: relative;
	top: 0.9rem;
	height: 35px;
	width: 100px;
	float: right;
	padding: 0.5rem;
}
.dot {
	height: 0.4rem;
	width: 0.4rem;
	margin: 0.1rem;
	position: relative;
	top: 3px;
	background-color: rgb(255, 255, 255);
	border-radius: 50%;
	display: inline-block;
}
.dot:nth-child(4n) {
	margin-right: 1rem !important;
}

#show-card-no{
	border-radius:5px;
	background-color:#FFFFFF;
	position: relative;
	top:2rem;
	left:11rem;
	height: 2.5rem;
	width:45%;
	font-size:0.7rem;
	font-weight: bold;
	z-index: -5;
	color:#01D167;	
}

.card--styles  {
	background-color: #536DFF;
	letter-spacing: 1px;
	width: 20rem;
	color: white;
	text-align: left;
	/* padding-left: 0.5rem; */
}
.card-body--styles {
	font-size: 0.8rem;
	font-weight: bold;
	padding-bottom: 0.5rem;
}

.carousel__slide--active div.card{
	background-color: #01d167;

}

 .carousel__slide--active div.card.frozen{
  box-shadow: 0 0 1rem 0 rgba(0, 0, 0, 0.459); 
  position: relative;
  z-index: 1;
  background: inherit;
  overflow: hidden;
  opacity: 0.5;
  
}
#show-card-no.frozen{
	opacity:0;
}

.carousel__slide--active div.card.frozen:before {
  content: "";
  position: absolute;
  background: inherit;
  z-index: -1;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  box-shadow: inset 0 0 2000px rgb(255, 255, 255);
  filter: blur(10px);
  margin: -10px;
}
.carousel__slide > .carousel__item {
	/* height: 15rem; */
	margin-left:10px;
	transform: scale(1);
	opacity: 0.5;
	transition: 0.5s;
}
.carousel__slide--visible > .carousel__item {
	opacity: 1;
	transform: rotateY(0);
}
.carousel__slide--next > .carousel__item {
	transform: scale(0.9) translate(-23px);
}
.carousel__slide--prev > .carousel__item {
	transform: scale(0.9) translate(15px);
}
/* .carousel__slide--active > .carousel__item {
	transform: scale(1.1);
} */
</style>
