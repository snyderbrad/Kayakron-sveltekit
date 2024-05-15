<script lang="ts">
	import { Hamburger } from 'svelte-hamburgers';
	import { quintOut } from 'svelte/easing';
	import { fade, draw, fly } from 'svelte/transition';
	import { expand } from './custom-transitions.js';
	import { inner, outer } from './shape.js';
	import { onMount } from 'svelte';
	export const prerender = true;
	export const ssr = true;

	let open;
	let visible = false;
	onMount(() => {
		visible = true;
		scrollSlides(1);
	});

	let slideIndex = 1;
	let imageUrl = 'welcome-photo.jpg';
	let images = ['pic1-600.jpg', 'pic2-600.jpg', 'pic3-600.jpg'];
	let infographic = '/Infographic.pdf';
	const plusSlides = async () => scrollSlides((slideIndex += 1));
	const plusSlidesDown = async () => scrollSlides((slideIndex -= 1));
	const currentSlide = async (slide) => scrollSlides(slide);

	function scrollSlides(n) {
		let i;
		let slides = document.getElementsByClassName('slide-frame');
		let dots = document.getElementsByClassName('dot');
		if (n > slides.length) {
			slideIndex = 1;
		}
		if (n < 1) {
			slideIndex = slides.length;
		}
		for (i = 0; i < slides.length; i++) {
			slides[i].setAttribute('style', 'display:none;');
		}
		for (i = 0; i < dots.length; i++) {
			dots[i].className = dots[i].className.replace(' active', '');
		}
		slides[slideIndex - 1].setAttribute('style', 'display:block;');
		dots[slideIndex - 1].className += ' active';
	}
</script>

<link
	rel="stylesheet"
	href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css"
/>

<main>
	<div class="align-horizontally">
		<div class="topnav">
			<Hamburger bind:open />
			{#if open}
				<a href="tel:3306060543" class="fa fa-mobile-phone header-text">(330)606-0543</a>
				<a target="_blank" class="header-text" rel="noopener noreferrer" href={infographic}>How To</a>
			{/if}
		</div>
		{#if visible}
			<svg
				id="logo-svg"
				width="100vw"
				height="50vh"
				viewBox="0 0 623 396"
				fill="none"
				xmlns="http://www.w3.org/2000/svg"
			>
				<g out:fade={{ duration: 200 }} opacity="1">
					<path
						in:expand={{ duration: 10, easing: quintOut }}
						style="stroke: #6f4930; fill: #56903a; stroke-width: 50;"
						d={outer}
					/>
					<path in:draw={{ duration: 11000 }} style="stroke:#FFFFFF; stroke-width: 1.4" d={inner} />
				</g>
			</svg>
		{/if}
		<div class="about-column">
			<img class="about" src={imageUrl} alt="" />
			<p>
				<b> Kayakron </b> is a kayak outfitter located in Akron, Ohio. We provide a fully equipped kayak
				so you can enjoy your time on the water. Our drop-off service includes a licensed kayak, paddle,
				PFD (life preserver), as well as dry storage. For an hourly or daily rate, our kayaks can be
				enjoyed at many of our local lakes, rivers, and ponds. Call us today to get on the river!
			</p>
		</div>
		<div class="slideshow-container">
			{#each images as { image }, i}
				<div class="slide-frame fade">
					<div class="numbertext">{i + 1} / {images.length}</div>
					<img src={images[i]} alt="" class="slide-image" />
				</div>
			{/each}
			<div id="arrows-container">
				<div id="prev-arrow" on:click={plusSlidesDown}>
					<p>&#10094;</p>
				</div>
				<div id="next-arrow" on:click={plusSlides}>
					<p>&#10095;</p>
				</div>
			</div>
			<br />
			{#each images as { slide }, i}
				<div id="dots" style="text-align:center">
					<span class="dot" on:click={currentSlide(i + 1)} />
				</div>
			{/each}
		</div>
	</div>
</main>
<div class="bottom-info">
	<a href="tel:3306060543" class="fa fa-mobile-phone">&nbsp;&nbsp;&nbsp;(330) 606-0543</a>
	<a href="mailto:kayakron@gmail.com" class="fa fa-envelope">kayakakron@gmail.com</a>
</div>

<style scoped>
	:global(body) {
		background-color: #c5b867;
	}

	.topnav {
		position: absolute;
		align-items: center;
		top: 0px;
		left: 0;
		width: 95vw;
		overflow: hidden;
		display: flex;
		flex-direction: row;
		gap: 10px;
	}

	.align-horizontally {
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #c5b867;
		max-width: 100vw;
		margin: 0px;
		padding: 0px;
		border-radius: 25px;
	}

	.about-column img {
		float: right;
	}

	.about {
		width: 40vw;
		padding-right: 10px;
	}

	.about-column {
		width: 100vw;
		font-size: 2.5em;
		margin-top: 50px;
		width: 100vw;
		color: darkslategrey;
	}

	.bottom-info {
		/* height: 40px; */
		width: 100%;
		max-height: 10%;
		position: fixed;
		text-align: center;
		z-index: 3;
		bottom: 0;
		left: 0;
		background-color: #495d4e;
	}

	.bottom-info a {
		max-height: 10%;
		padding: 10px;
		text-decoration: none;
		font-size: 1.5em;
		color: #c5b867;
	}

	.slideshow-container {
		max-width: 100vw;
		width: 100vw;
		position: relative;
		display: flex;
		justify-content: center;
		margin: 0px;
		padding-top: 5vh;
	}

	.dot {
		visibility: hidden;
	}

	.slide-image {
		width: 40vw;
		max-width: 40vw;
		max-height: 100vh;
		height: auto;
	}

	.slide-frame {
		padding-bottom: 10vh;
		position: absolute;
		display: none;
	}

	#arrows-container {
		position: absolute;
		bottom: 0;
		width: 100vw;
	}

	#prev-arrow {
		cursor: pointer;
		position: absolute;
		top: 50%;
		left: 25%;
		width: auto;
		color: white;
		font-weight: bold;
		font-size: 5em;
		transition: 0.6s ease;
		border-radius: 0 3px 3px 0;
		user-select: none;
	}

	#next-arrow {
		cursor: pointer;
		position: absolute;
		top: 50%;
		right: 25%;
		width: auto;
		color: white;
		font-weight: bold;
		font-size: 5em;
		transition: 0.6s ease;
		border-radius: 0 3px 3px 0;
		user-select: none;
	}

	.numbertext {
		color: #495d4e;
		font-size: 12px;
		padding: 8px 12px;
		z-index: 0;
	}

	.dot {
		cursor: pointer;
		height: 15px;
		width: 15px;
		margin: 0 2px;
		background-color: #bbb;
		border-radius: 50%;
		display: inline-block;
		transition: background-color 0.6s ease;
	}

	.dot:hover {
		background-color: #030202;
		opacity: 25%;
	}

	#dots {
		padding-top: 15px;
	}

	.fade {
		-webkit-animation-name: fade;
		-webkit-animation-duration: 0.2s;
		animation-name: fade;
		animation-duration: 0.2s;
	}

	.header-text {
		color: white;
		border-top: 1px solid #cccccc;
		border-right: 1px solid #333333;
		border-bottom: 1px solid #333333;
		border-left: 1px solid #cccccc;
		justify-content: center;
		background-color: #495d4e;
		font-size: 1rem;
		line-height: 25px;
		border-radius: 25px;
		padding: 5px;
		font-family: 'Cabin Condensed', sans-serif;
	}

	@keyframes animate {
		0% {
			transform: translateY(0px);
		}

		20% {
			transform: translateY(-20px);
		}

		40%,
		100% {
			transform: translateY(0px);
		}
	}

	@-webkit-keyframes fade {
		from {
			opacity: 0.4;
		}
		to {
			opacity: 1;
		}
	}

	@keyframes fade {
		from {
			opacity: 0.4;
		}
		to {
			opacity: 1;
		}
	}

	@media screen and (max-width: 500px) {
		.about-column {
			font-size: 1.5em;
		}

		.about {
			width: 50vw;
		}

		.topnav a {
			float: none;
			display: block;
			text-align: left;
		}
		.bottom-info a {
			font-size: 1em;
			display: inline-block;
			text-align: left;
		}
	}

	#logo-svg {
		padding-top: 10vh;
	}

	path {
		fill: #000000;
		opacity: 1;
	}
</style>
