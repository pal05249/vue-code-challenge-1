<template>
	<div class="row">
		<div class="col-lg-3">
			<div class="text-white sidebar">
				<div class="logo">
					<a href="/">
						<img :src="logo" alt="logo" />
					</a>
					<p class="logo-text">
						Trusted way of banking for 3,000+ SMEs and startups in Singapore
					</p>
				</div>

				<div class="navigation">
					<ul class="nav nav-pills flex-column">
						<li class="nav-item mb-5">
							<a href="#" class="text-white" aria-current="page"
								><img :src="home_icon" style="padding-right: 1rem" alt="" />
								Home
							</a>
						</li>
						<li class="nav-item mb-5">
							<a href="#" class="activated">
								<img :src="cards_icon" style="padding-right: 1rem" alt="" />
								Cards
							</a>
						</li>
						<li class="nav-item mb-5">
							<a href="#" class="text-white">
								<img :src="payments_icon" style="padding-right: 1rem" alt="" />
								Payments
							</a>
						</li>
						<li class="nav-item mb-5">
							<a href="#" class="text-white">
								<img :src="credits_icon" style="padding-right: 1rem" alt="" />
								Credits
							</a>
						</li>
						<li class="nav-item mb-5">
							<a href="#" class="text-white">
								<img :src="settings_icon" style="padding-right: 1rem" alt="" />
								Settings
							</a>
						</li>
					</ul>
				</div>
			</div>
		</div>
		<div class="col-lg-9">
			<div class="row">
				<div class="right-content">
					<p>Available balance</p>
					<div class="d-flex align-items-center justify-content-between">
						<div class="d-flex align-items-center">
							<span
								class="badge m-2 py-1 px-2"
								style="background-color: #01d167"
								>S$</span
							>
							<b style="font-size: 2rem">3,000</b>
						</div>

						<button
							class="button d-flex align-items-center justify-content-evenly"
						>
							<img :src="add_icon" alt="" />
							<span>New card</span>
						</button>
					</div>
				</div>
			</div>
			<div class="row">
				<div class="card w-100">
					<div class="card-title">HelloWorld</div>
					<div class="card-body">Helllllo</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: "HelloWorld",
	props: {
		msg: String,
	},
	data() {
		return {
			logo: require("../assets/asset/Aspire_Logo.svg"),
			home_icon: require("../assets/asset/Logo-1.svg"),
			cards_icon: require("../assets/asset/Card.svg"),
			payments_icon: require("../assets/asset/Payments.svg"),
			credits_icon: require("../assets/asset/Credit.svg"),
			settings_icon: require("../assets/asset/Account.svg"),
			add_icon: require("../assets/asset/add.svg"),
		};
	},
	computed: {
		flex: function () {
			if (
				/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/i.test(
					navigator.userAgent
				)
			) {
				return "flex-row";
			} else return "flex-column";
		},
	},
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.sidebar {
	width: 100%;
	padding: 3rem;
	height: 100vh;
	background-color: #0c365a;
	order: 1;
}
.logo {
	text-align: left;
}
.logo-text {
	opacity: 0.3;
	margin-top: 1rem;
	font-size: 1rem;
}
a {
	text-decoration: none;
}
.right-content {
	padding: 3rem;
	order: 2;
}
a.activated {
	font-weight: bold;
	color: #01d167;
}
.navigation {
	margin-top: 6.25rem;
}
.button {
	border-radius: 4px;
	width: 8rem;
	background-color: #325baf;
	font-size: 0.9rem;
	padding: 0.25rem;
	color: white;
}
</style>
