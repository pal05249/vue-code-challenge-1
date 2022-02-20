<template>
	<div class="row">
		<!-- side nav bar -->
		<div class="col-lg-3 d-lg-flex">
			<nav class="main-nav">
				<div class="logo">
					<a href="/">
						<img :src="logo" alt="logo" />
					</a>
					<p class="logo-text">
						Trusted way of banking for 3,000+ SMEs and startups in Singapore
					</p>
				</div>
				<ul>
					<li class="has-subnav">
						<a href="#">
							<i class="fa"> <img :src="home_icon" alt="home_icon" /></i>
							<span class="nav-text"> Home </span>
						</a>
					</li>

					<li class="has-subnav">
						<a href="#">
							<i class="fa">
								<img :src="cards_icon" alt="cards_icon" />
							</i>
							<span class="nav-text active"> Cards </span>
						</a>
					</li>

					<li class="has-subnav">
						<a href="#">
							<i class="fa">
								<img :src="payments_icon" alt="payments_icon" />
							</i>
							<span class="nav-text"> Payments </span>
						</a>
					</li>

					<li class="has-subnav">
						<a href="#">
							<i class="fa">
								<img :src="credits_icon" alt="credits_icon" />
							</i>
							<span class="nav-text"> Credits </span>
						</a>
					</li>
					<li class="has-subnav">
						<a href="#">
							<i class="fa">
								<img :src="settings_icon" alt="settings_icon"
							/></i>
							<span class="nav-text"> Settings </span>
						</a>
					</li>
				</ul>
			</nav>
		</div>
		<!-- right content -->
		<div class="container">
			<div class="content col-sm-12 col-lg-9">
				<div class="row">
					<div class="right-content">
						<p class="mt-3 px-3">
							Account balance
							<img style="float: right" :src="logo_icon" alt="" />
						</p>

						<div class="d-flex align-items-center justify-content-between">
							<div class="d-flex align-items-center px-2">
								<span
									class="badge m-2"
									style="background-color: #01d167; z-index: 0"
									>S$</span
								>
								<b style="font-size: 1.5rem">3,000</b>
							</div>

							<a class="new-button" @click="showModal">
								<img :src="box_icon" alt="add-icon" />
								<span style="padding-right: 1rem">New card</span>
							</a>
						</div>
					</div>
				</div>
				<div class="row">
					<div class="col-sm-12">
						<ul class="nav">
							<li
								class="custom-tab"
								@click.prevent="setActive('debit_cards')"
								:class="{ active: isActive('debit_cards') }"
							>
								My debit cards
							</li>
							<li
								class="custom-tab"
								@click.prevent="setActive('all_cards')"
								:class="{ active: isActive('all_cards') }"
							>
								All company cards
							</li>
						</ul>
						<div class="py-3" id="myTabContent">
							<div
								:class="{ 'active show': isActive('debit_cards') }"
								id="debit_cards"
							>
								<!-- card component---------------------------------------- -->

								<carousel
									:card_lists="card_lists"
									ref="carousel-item"
									@mounted="execute(value)"
									v-model="currentSlide"
									
								/>
							</div>
						</div>
					</div>
				</div>
			</div>
			<div class="col-sm-12 text-dark" id="scrollable">
				<ul class="scroll-nav text-center">
		
					<li @click="freezeCard()">
						<img :src="freeze_card_icon" alt="" />
						<p>{{freeze_status}}</p>
					</li>
					<li>
						<img :src="set_spend_limit_icon" alt="" />
						<p>Set Spend limit</p>
					</li>
					<li>
						<img :src="gpay_icon" alt="" />
						<p>Add to Gpay</p>
					</li>
					<li>
						<img :src="replace_card_icon" alt="" />
						<p>Replace Card</p>
					</li>
					<li @click="showModal2()">
						<img :src="deactivate_card_icon" alt="" />
						<p>Cancel Card</p>
					</li>
				</ul>

				<div class="card bg-white">
					<div class="card new-card m-3">
						<div class="d-flex justify-content-between mx-3 my-3">
							<div>
								<img :src="card_details_icon" class="p-2" alt="" />
								<span class="text-dark-blue" style="font-weight: bold"
									>Card details</span
								>
							</div>

							<img :src="down_arrow_icon" alt="" />
						</div>
					</div>

					<div class="card new-card m-3">
						<div class="d-flex justify-content-between mx-3 my-3">
							<div>
								<img :src="recent_transactions_icon" class="p-2" alt="" />
								<span class="text-dark-blue" style="font-weight: bold"
									>Recent transactions</span
								>
							</div>

							<img :src="down_arrow_icon" @click="show_collapsible()" alt="" />
						</div>

						<div v-show="Show == true">
							<div
								style="background-color: white; width: 100%"
								v-for="(item, index) in this.recent_transactions"
								:key="index"
							>
								<div class="d-flex flex-row justify-content-evenly pt-3">
									<div
										class="col-sm-2 p-4"
										:style="{ 'background-color': item.bg }"
										style="
											border-radius: 100%;

											margin-bottom: 2rem;
										"
									>
										<img :src="item.icon" alt="" />
									</div>
									<div class="col-sm-8">
										<p
											style="
												font-weight: bold;
												font-size: 1rem;
												margin-bottom: 0;
											"
										>
											{{ item.title }}
										</p>
										<p style="opacity: 0.7; font-size: 0.9rem">
											{{ item.date }}
										</p>
										<p>
											<img
												:src="card_icon"
												style="background-color: #325baf; border-radius: 35%"
												class="p-2"
												alt="card_icon"
											/>
											<span
												style="
													font-size: 0.8rem;
													color: #325baf;
													font-weight: bold;
													margin-left: 2px;
												"
												>{{ item.action }}</span
											>
										</p>
									</div>
									<div class="col-sm-2">
										<p
											style="font-weight: bold"
											:style="[
												item.price > 0
													? { color: '#01D167' }
													: { color: '#222222' },
											]"
										>
											{{
												item.price > 0 ? "+S$" + item.price : "-S$" + item.price
											}}
											<img :src="next_icon" class="p-2" alt="" />
										</p>
									</div>
								</div>
								<hr />
							</div>
						</div>
					</div>
				</div>
			</div>
		</div>
		<!-- Modal for adding new card ---------------------------------------------->
		<Modal v-show="isModalVisible" @close="closeModal">
			<template v-slot:header>Add a new card </template>

			<template v-slot:body>
				<div class="form-group">
					<label for="name">Name of the card holder</label>
					<input
						type="text"
						id="name"
						class="form-control"
						v-model="card_holder_name"
						title="Only alphabets,space and dots"
					/>
					 <p v-show="this.errors.length">
    					<ul>
      					<li v-for="error in errors" class="danger" :key="error"><span >{{ error }}</span></li>
    					</ul>
  					</p>
				</div>
			</template>

			<template v-slot:footer>
				<button
					type="button"
					class="btn bg-green text-white"
					@click="
						addCard(card_holder_name);
						
					"
				>
					Add
				</button>
			</template>
		</Modal>
		<!-- Modal for cancelling card  -------------------------------------------------------->
		<Modal v-show="isModalVisible2" @close="closeModal2">
			<template v-slot:header>Cancel Card </template>

			<template v-slot:body>
				<p>Please confirm if you want to cancel this card?</p>
			</template>

			<template v-slot:footer>
				<button type="button" class="btn btn-danger" @click="deleteCard();closeModal2()">
					Yes
				</button>
				<button type="button" class="btn btn-secondary" @click="closeModal2()">
					No
				</button>
			</template>
		</Modal>
	</div>
</template>

<script>
import Modal from "../components/Modal.vue";
import carousel from "../components/Carousel.vue";
export default {
	name: "Dashboard",
	components: {
		Modal,
		carousel,
	},

	data() {
		return {
			errors: [],
			data: null,
			currentSlide: 0,
			card_holder_name: "",
			activeItem: "debit_cards",
			isModalVisible: false,
			isModalVisible2: false,
			Show: false,
			// icons-------------------------------------
			visa_logo: require("../assets/asset/Visa Logo.svg"),
			logo_white: require("../assets/asset/Logo-2.svg"),
			logo_icon: require("../assets/asset/Logo.svg"),
			logo: require("../assets/asset/Aspire_Logo.svg"),
			home_icon: require("../assets/asset/Logo-1.svg"),
			cards_icon: require("../assets/asset/Card.svg"),
			payments_icon: require("../assets/asset/Payments.svg"),
			credits_icon: require("../assets/asset/Credit.svg"),
			settings_icon: require("../assets/asset/Account.svg"),
			add_icon: require("../assets/asset/add.svg"),
			box_icon: require("../assets/asset/box.svg"),
			freeze_card_icon: require("../assets/asset/Freeze card.svg"),
			set_spend_limit_icon: require("../assets/asset/Set spend limit.svg"),
			gpay_icon: require("../assets/asset/GPay.svg"),
			replace_card_icon: require("../assets/asset/Replace card.svg"),
			deactivate_card_icon: require("../assets/asset/Deactivate card.svg"),
			down_arrow_icon: require("../assets/asset/down-arrow.svg"),
			card_details_icon: require("../assets/asset/Group 11889.svg"),
			next_icon: require("../assets/asset/next.svg"),
			card_icon: require("../assets/asset/business-and-finance.svg"),
			recent_transactions_icon: require("../assets/asset/Group 11889-1.svg"),
			// ------------------------------------------------------------------
			card_lists: [],

			recent_transactions: [
				{
					title: "Hamleys",
					date: "20 May 2020",
					price: 150,
					action: "Refund to debit card",

					icon: require("../assets/asset/file-storage.svg"),
					bg: "#009DFF1A",
				},
				{
					title: "Hamleys",
					date: "20 May 2020",
					price: -150,
					action: "Charged to debit card",
					icon: require("../assets/asset/flights.svg"),
					bg: "#00D6B51A",
				},
				{
					title: "Hamleys",
					date: "20 May 2020",
					price: -150,
					action: "Charged to debit card",
					icon: require("../assets/asset/megaphone.svg"),
					bg: "#F251951A",
				},
				{
					title: "Hamleys",
					date: "20 May 2020",
					price: -150,
					action: "Charged to debit card",
					icon: require("../assets/asset/file-storage.svg"),
					bg: "#009DFF1A",
				},
			],
		};
	},
	created() {
		this.setData();
	
	},
	computed: {
		freeze_status: function () {
			if (this.card_lists.length!==0)
				{
				if(this.card_lists[this.currentSlide].isFrozen=="frozen")
				return "UnFreeze card";}
		
				 return "Freeze card";
			
		},
	},
	methods: {
		setData() {
			if (localStorage.cards == null) {
				if (this.card_lists.length == 0) {
					this.card_lists = [
						{
							name: "Mark henry",
							exp_date: this.getRandomExpDate(),
							isFrozen: "",
						},
					];
					localStorage.cards = JSON.stringify(this.card_lists);
				}
			} else {
				this.card_lists = JSON.parse(localStorage.cards);
			}
		},
		getRandomExpDate() {
			return `${Math.floor(Math.random() * (12 - 0 + 1)) + 1}/${
				Math.floor(Math.random() * (30 - 20 + 1)) + 20
			}`;
		},
		// nav tabs
		isActive(menuItem) {
			return this.activeItem === menuItem;
		},
		setActive(menuItem) {
			this.activeItem = menuItem;
		},
		show_collapsible() {
			this.Show = !this.Show;
		},
		// Modal-adding card
		showModal() {
			this.isModalVisible = true;
		},
		closeModal() {
			this.isModalVisible = false;
		},
		// Modal-cancelling card
		showModal2() {
			this.isModalVisible2 = true;
		},

		closeModal2() {
			this.isModalVisible2 = false;
		},

		addCard(name) {
			this.errors = [];
			const regex = /^(?:[a-zA-Z][a-zA-Z\s\.]*){2,}$/;

			if (regex.exec(name)) {
				this.card_lists.push({
					name: name,
					exp_date: this.getRandomExpDate(),
					isFrozen: "",
				});
				localStorage.cards = JSON.stringify(this.card_lists);

				this.closeModal();
			} else {
				this.errors.push("Only alphabets (min 2 letters) with dot and spaces allowed!");

				setTimeout(
					function () {
						this.errors = [];
					}.bind(this),
					4000
				);
			}
			this.card_holder_name = "";
		},

		deleteCard() {
			this.card_lists=JSON.parse(localStorage.cards)
			this.card_lists.splice(this.currentSlide, 1);
			this.currentSlide=0;
			localStorage.cards = JSON.stringify(this.card_lists);
			this.isModalVisible2=false;

		},
		freezeCard() {
			if (this.card_lists[this.currentSlide].isFrozen == "frozen") {
				this.card_lists[this.currentSlide].isFrozen = "";
			} else {
				
				this.card_lists[this.currentSlide].isFrozen = "frozen";
			}
			localStorage.cards = JSON.stringify(this.card_lists);
		},
	},
};
</script>




<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.danger {
	color: red;
	font-weight: bold;
	font-size: 0.8rem;
	list-style-type: none;
}
#debit-card {
	position: relative;
	top: 2rem;
	border-radius: 1rem;
	height: 14rem;
	width: 22rem;
	margin: 0.5rem auto;
}
.dot {
	height: 0.5rem;
	width: 0.5rem;
	margin: 0.2rem;
	position: relative;
	top: 3px;
	background-color: rgb(255, 255, 255);
	border-radius: 50%;
	display: inline-block;
}
.dot:nth-child(4n) {
	margin-right: 1rem !important;
}
hr {
	width: 70%;
	border: 0;
	margin: 0 auto;
	height: 1px;
	background: #000;
	opacity: 0.2;
}

.text-dark-blue {
	color: #0c365a;
}
.bg-dark-blue {
	background-color: #0c365a;
}
.bg-green {
	background-color: #01d167;
}
.fa-2x {
	font-size: 2rem;
}

.is-hidden {
	display: none;
}
.fa {
	position: relative;
	text-align: center;
	vertical-align: middle;
	font-size: 2rem;
}

.main-nav {
	background: #0c365a;
	border-right: 1px solid #e5e5e5;
	position: fixed;
	z-index: 1000;
	color: white;
}
.main-nav > ul {
	margin: 0rem 2rem;
}

nav ul,
nav li {
	outline: 0;
	margin: 0;
	padding: 0;
}
.main-nav li:hover > a,
nav.main-nav li.active > a {
	color: #fff;
	background-color: #919191;
}
.custom-tab {
	font-size: 0.8rem;
	font-weight: bold;
	margin: 0rem 1rem;
	background: transparent !important;
	color: white;
	opacity: 0.5;
	border-radius: 0px !important;
}
.custom-tab.active {
	opacity: 1;
	border-bottom: 2px solid #23cefd !important;
}
.main-nav .nav-text,
.main-nav li > a {
	font-family: "Roboto", sans-serif;
}

.main-nav li > a {
	border-collapse: collapse;
	border-spacing: 0;
	color: white;
	font-size: 1.03rem;
	text-decoration: none;
}
/* for tab screens */
@media only screen and (min-width: 35em) and (max-width: 992px) {
	.fa {
		display: table-cell;
		width: 5rem;
		height: 5rem;
	}

	nav.main-nav {
		width: 24%;
		overflow: visible;
	}
	.main-nav:hover,
	nav.main-nav.expanded {
		width: 15em;
		overflow: visible;
	}
	.main-nav {
		top: 0;
		bottom: 0;
		height: 100%;
		left: 0;
		width: 5rem;
		overflow: hidden;
		-webkit-transition: width 0.05s linear;
		transition: width 0.05s linear;
		-webkit-transform: translateZ(0) scale(1, 1);
	}

	.main-nav li {
		text-decoration: none;
		position: relative;
		display: block;
		width: 3rem;
	}
	.main-nav li > a {
		position: relative;
		display: table;
		-webkit-transform: translateZ(0) scale(1, 1);
		-webkit-transition: all 0.1s linear;
		transition: all 0.1s linear;
	}

	.main-nav .nav-text {
		position: relative;
		display: table-cell;
		vertical-align: middle;
		width: 10rem;
	}
	.logo {
		margin: 3rem;
	}
	.logo-text {
		display: none;
	}
}
/* for large screens */
@media (min-width: 992px) {
	.fa {
		display: table-cell;
		width: 5rem;
		height: 5rem;
	}
	.scroll-nav {
		border-top-left-radius: 25px;
		border-top-right-radius: 25px;
		background-color: #edf3ff;
		background: linear-gradient(#edf3ff);
		display: flex;
		flex-direction: column;
		justify-content: justify-content-evenly;
		font-size: 0.7rem;
		padding: 0 1rem;
		list-style-type: none;
		color: #0c365a;
		font-weight: 500;
	}

	nav.main-nav {
		width: 24%;
		overflow: visible;
	}

	.main-nav {
		order: 1;
		top: 0;
		bottom: 0;
		height: 100%;
		left: 0;
		width: 5rem;
		overflow: hidden;
		-webkit-transition: width 0.05s linear;
		transition: width 0.05s linear;
		-webkit-transform: translateZ(0) scale(1, 1);
	}

	.main-nav li {
		position: relative;
		display: block;
		width: 18rem;
	}
	.main-nav li > a {
		position: relative;
		display: table;
		-webkit-transform: translateZ(0) scale(1, 1);
		-webkit-transition: all 0.1s linear;
		transition: all 0.1s linear;
	}

	.main-nav .nav-text {
		position: relative;
		display: table-cell;
		vertical-align: middle;
		width: 10rem;
	}
	.logo {
		margin: 3rem;
	}
	.logo-text {
		opacity: 0.3;
		margin-top: 1rem;
		font-size: 1rem;
	}
	.container {
		order: 2;
	}
}
/* for mobile devices */
@media (max-width: 560px) {
	.new-card {
		border: 1px solid #f5f5f5;
		filter: drop-shadow(0 0 #0000000a blur);
		background-color: #fafcff;
	}
	#scrollable {
		/* border-top-right-radius: 25px; */
		width: 100%;
		z-index: 2;
		position: relative;
		top: 10rem;
		/* bottom: 5rem; */
		height: 100%;
	}
	.content {
		position: sticky;
		top: 0;
		z-index: 0;
	}
	ul {
		margin: 0;
		padding: 0;
	}
	.scroll-nav {
		border-top-left-radius: 25px;
		border-top-right-radius: 25px;
		background-color: #edf3ff;
		background: linear-gradient(#edf3ff);
		display: flex;
		justify-content: justify-content-evenly;
		font-size: 0.7rem;
		widows: 100%;
		padding: 0 1rem;
		list-style-type: none;
		color: #0c365a;
		font-weight: 500;
	}
	.scroll-nav li {
		margin: 1rem 0.5rem;
		justify-content: center;
		/* text-align: center; */
		align-items: center;
	}

	.main-nav {
		background: #ffffff;
		border-right: 1px solid #e5e5e5;
		/* position: fixed; */
		/* position: relative; */
		z-index: 3;
		margin: 0;
		/* left: 0; */
		bottom: 0;
		/* height: 5em; */
		width: 100%;
	}
	.container {
		background-color: #0c365a;
		height: 100vh;
		color: white;
		margin: 0;
		/* padding: 1rem; */
	}
	.main-nav ul {
		display: table;
		margin: 0;
		width: 100%;
		order: 2;
		text-align: center;
		/* position: sticky; */
	}

	.main-nav li {
		float: left;
		width: 20%;
		list-style-type: none;
		text-align: center;
	}

	.main-nav a {
		display: block;
		/* padding: 5px; */
		height: 74px;
	}

	.main-nav i,
	.main-nav span {
		display: block;
		color: #dddddd;
	}

	.main-nav span {
		font-size: 0.75rem;
	}
	.logo {
		display: none;
	}
	.right-content {
		z-index: 999;
		/* padding: 1rem; */
	}
	.new-button {
		display: flex;
		border: none;
		width: 8rem;
		font-weight: bold;
		background-color: #0c365a;
		font-size: 0.8rem;
		justify-content: flex-end;
		align-items: center;
		/* padding: 0.25rem; */
		color: #23cefd;
		text-decoration: none;
	}
	.nav-text.active {
		color: #01d167;
	}
	.nav-text {
		font-weight: bold;
	}
}
</style>
