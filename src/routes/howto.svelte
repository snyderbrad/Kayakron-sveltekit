<script lang="ts">
    export const prerender = true;
    export const ssr = true;
	export let imageSlide;
	let imageState = imageSlide;
	let imageUrl = 'logo.jpg';
	let image1 = 'pic1.jpg/';
	let image2 = 'pic2.jpg/';
	let image3 = 'pic3.jpg/';
	const handleImageClick = async () => console.log('Click!');
	const isMobile = async () =>
		navigator.userAgent.match(/Android|webOS|iPhone|iPad|iPod|BlackBerry|IEMobile|Opera Mini/)
			? true
			: false;
</script>

<div>
	<p>how to</p>
</div>

<style scoped>
	.align-vertically {
		background-color: #c5b867;
		display: flex;
		align-items: top;
		height: 100%;
		width: 100%;
	}

	.slider-column {
		width: 1350px;
		height: 600px;
	}

	.slider-container {
		position: fixed;
		z-index: 0;
	}

	.slider_frame {
		overflow: hidden;
		height: 1500px;
		width: 450px;
	}

	.slider-images {
		height: 600px;
		width: 1350px;
		animation-name: slide_animation;
		-webkit-animation-name: slide_animation;
		animation-duration: 12s;
		-webkit-animation-duration: 12s;
		animation-iteration-count: infinite;
		-webkit-animation-iteration-count: infinite;
		animation-direction: alternate-reverse;
		-webkit-animation-direction: alternate-reverse;
		-webkit-animation-play-state: running;
		animation-play-state: running;
	}

	.slide-image {
		max-width: 100%;
		float: left;
		width: 450px;
		height: auto;
		padding-top: 150px;
	}

	.img-container {
		height: 500px;
		width: 450px;
		/* margin-top: 200px;/s */
		float: left;
	}

	.logo {
		width: auto;
		max-height: 110%;
		float: left;
	}

	.about-column {
	}

	.about {
		font-size: 21px;
		text-align: center;
		padding-left: 21%;
		padding-right: 21%;
		height: 200px;
	}

	.welcome {
		font-size: 34px;
		padding-top: 0px;
		text-align: center;
		padding-left: 21%;
		padding-right: 21%;
	}

	.phone {
		font-size: 34px;
		padding-top: 0px;
		text-align: center;
		padding-left: 21%;
		padding-right: 21%;
	}

	.intro {
		width: 100%;
		padding-top: 30px;
		font-size: 34px;
	}

	.bottom-info {
		height: 40px;
		width: 100%;
		max-height: 5%;
		position: fixed;
		z-index: 3;
		bottom: 0;
		left: 0;
		background-color: #495d4e;
	}

	.bottom-info p {
		padding: 0px 50px 0px 10px;
		text-decoration: none;
		font-size: 13px;
		color: #c5b867;
	}

	.topnav {
		height: 60px;
		width: 100%;
		position: fixed;
		z-index: 2;
		top: 0;
		left: 0;
		background-color: #495d4e;
		overflow-x: auto;
		padding-bottom: 10px;
		overflow: hidden;
	}

	.topnav a {
		padding: 6px 8px 6px 16px;
		text-decoration: none;
		margin-top: 10px;
		font-size: 25px;
		color: #c5b867;
		float: left;
	}

	.topnav a:hover {
		color: #f1f1f1;
	}

	@-webkit-keyframes slide_animation {
		0% {
			margin-left: 0px;
		}
		10% {
			margin-left: 0px;
		}
		20% {
			margin-left: -450px;
		}
		30% {
			margin-left: -450px;
		}
		40% {
			margin-left: -900px;
		}
		50% {
			margin-left: -900px;
		}
		60% {
			margin-left: -450px;
		}
		70% {
			margin-left: -450px;
		}
		80% {
			margin-left: -0px;
		}
		90% {
			margin-left: 0px;
		}
		100% {
			margin-left: 0px;
		}
	}
</style>
