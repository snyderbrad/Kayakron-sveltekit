<script lang="ts">
    export const prerender = true;
    export const ssr = true;
	import { onMount } from 'svelte';
	let ready = false;
	onMount(() => {
		ready = true;
		scrollSlides(1);
	});

    let letters = ['E', 'x', 'p', 'l', 'o', 'r', 'e', ' ', 'T', 'h', 'e', ' ', 'R', 'i', 'v', 'e', 'r', ''];
	let slideIndex = 1;
	let imageUrl = 'logo.jpg';
	let image1 = 'pic1-600.jpg';
	let image2 = 'pic2-600.jpg';
	let image3 = 'pic3-600.jpg';
	let image4 = 'pic4-600.jpg';
	let infographic = '/Infographic.pdf';
	let howto = 'howto.svelte';
	const plusSlides = async () => scrollSlides((slideIndex += 1));
	const plusSlidesDown = async () => scrollSlides((slideIndex -= 1));
	const currentSlideOne = async () => scrollSlides(1);
	const currentSlideTwo = async () => scrollSlides(2);
	const currentSlideThree = async () => scrollSlides(3);
	const currentSlideFour = async () => scrollSlides(4);
	const handleImageClick = async () => alert('coming soon!');

	function currentSlide(n) {
		scrollSlides((slideIndex = n));
	}

	function scrollSlides(n) {
		let i;
		let slides = document.getElementsByClassName('mySlides');
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
		<div id="welcome" class="header">
			<div class="topnav">
				<a href="tel:3306060543" id="phone" class="fa fa-mobile-phone">&nbsp;(330) 606-0543</a>
				<a target="_blank" id="howto" rel="noopener noreferrer" href={infographic}>How To</a>
            </div>
            <div class="wavy">
                {#each letters as letter, index}
                    <span style="--i:{index}">{letter}</span>
                {/each}
            </div>
		</div>
		<div class="about-column" id="about">
			<p class="about">
				<b> Kayakron </b> is a kayak outfitter located in Akron, Ohio. We provide a fully equipped kayak
				so you can enjoy your time on the water. Our drop-off service includes a licensed kayak, paddle,
				PFD (life preserver), as well as dry storage. For an hourly or daily rate, our kayaks can be
				enjoyed at many of our local lakes, rivers, and ponds. Call us today to get on the river!
			</p>
		</div>
		<div class="slideshow-container">
			<div class="mySlides fade">
				<div class="numbertext">1 / 4</div>
				{#if ready}
					<img src={image1} alt="" class="slide-image" />
				{/if}
			</div>

			<div class="mySlides fade">
				<div class="numbertext">2 / 4</div>
				<img src={image2} alt="" class="slide-image" />
			</div>

			<div class="mySlides fade">
				<div class="numbertext">3 / 4</div>
				<img src={image3} alt="" class="slide-image" />
			</div>
			<div class="mySlides fade">
				<div class="numbertext">4 / 4</div>
				<img src={image4} alt="" class="slide-image" />
			</div>
			<div class="prev" on:click={plusSlidesDown}>
				<p>&#10094;</p>
			</div>
			<div class="next" on:click={plusSlides}>
				<p>&#10095;</p>
			</div>
			<br />
			<div class="dots" style="text-align:center">
				<span class="dot" on:click={currentSlideOne} />
				<span class="dot" on:click={currentSlideTwo} />
				<span class="dot" on:click={currentSlideThree} />
				<span class="dot" on:click={currentSlideFour} />
			</div>
		</div>
		<div class="about-column" id="about">
			<img src={imageUrl} alt="" style="max-width: 50vw" />
		</div>
	</div>
</main>
<div class="bottom-info">
	<a href="tel:3306060543" class="fa fa-mobile-phone">&nbsp;&nbsp;&nbsp;(330) 606-0543</a>
	<a href="mailto:kayakron@gmail.com" class="fa fa-envelope">kayakakron@gmail.com</a
	>
</div>

<!-- </div> -->
<style scoped>
	:global(body) {
		background-color: #c5b867;
	}
	#phone {
		width: auto;
		padding: 3px;
		text-align: center;
		border-radius: 10px;
		background-color: #495d4e;
		color: #c5b867;
		text-decoration: none;
		font-size: 1em;
	}

	#howto {
		width: auto;
		padding: 3px;
		text-align: center;
		border-radius: 10px;
		background-color: #495d4e;
		color: #c5b867;
		text-decoration: none;
		font-size: 1em;
	}

	#welcome {
		color: #c5b867;
		max-width: 100vw;
		min-width: 65vw;
		max-width: 75vw;
		height: 50vh;
		max-height: 50vh;
		float: left;
		padding: 0px;
		margin: -10px;
		background-image: url('/welcome-photo.jpg');
		background-position: center;
		background-repeat: no-repeat; /* Do not repeat the image */
		background-size: cover;
		font-family: 'Cabin Condensed', sans-serif;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.topnav {
		position: absolute;
		top: 0px;
		left: 0;
		width: 95vw;
		font-size: 1.5em;
		overflow: hidden;
		padding: 20px 10px;
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
		text-align: center;
	}

	#phone {
		text-align: center;
		align-content: center;
		padding-right: 10px;
		padding-left: 12px;
	}

	.about-column {
		margin-top: 50px;
		align-content: center;
		/* background-color: #c5b867; */
		width: 100%;
		color: darkslategrey;
	}

	.about {
		text-align: center;
		font-size: 1.5em;
		margin-left: 25px;
		margin-right: 25px;
		padding-left: 13%;
		padding-right: 13%;
		/* padding-top: 10px; */
		/* height: 100%; */
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
		/* margin: auto; */
		margin: 0px;
		padding-top: 5vh;
	}

    .dot {visibility: hidden;}

	.slide-image {
		max-height: 100vh;
		max-width: 100vw;
	}
    main {
        position: absolute; left: 0px;max-width: 100vw;
    }

    .mySlides {
		display: none;
	}

	/* Next & previous buttons */
	.prev,
	.next {
		cursor: pointer;
		position: absolute;
		top: 50%;
		width: auto;
		margin-top: -30vh;
		padding: 100px;
		color: white;
		font-weight: bold;
		font-size: 5em;
		transition: 0.6s ease;
		border-radius: 0 3px 3px 0;
		user-select: none;
		-webkit-tap-highlight-color:transparent;
	}

	/* Position the "next button" to the right */
	.next {
		right: 0;
		border-radius: 3px 0 0 3px;
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

	.dots {
		padding-top: 15px;
	}

	.dot:hover {
		background-color: #030202;
		opacity: 25%;
	}

	.fade {
		-webkit-animation-name: fade;
		-webkit-animation-duration: 0.2s;
		animation-name: fade;
		animation-duration: 0.2s;
	}

	.header a {
		float: left;
		color: black;
		background-color: #495d4e;
		text-align: center;
		padding: 25px;
		text-decoration: none;
		font-size: 18px;
		line-height: 25px;
		border-radius: 25px;
	}

    .wavy {
        position: relative;
    }

     .wavy span {
        position: relative;
        display: inline-block;
        color: #fff;
        font-size: 2em;
        text-transform: uppercase;
        animation: animate 2s ease-in-out infinite;
        animation-delay: calc(0.1s * var(--i));
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
		.header a {
			float: none;
			display: block;
			text-align: left;
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
		#welcome {
			height: 50vh;
		}
	}


</style>
