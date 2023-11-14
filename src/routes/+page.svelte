<script lang="ts">
    import { Hamburger } from 'svelte-hamburgers';

    let open;
    import { quintOut } from 'svelte/easing';
	import { fade, draw, fly } from 'svelte/transition';
	import { expand } from './custom-transitions.js';
	import { inner, outer } from './shape.js';

	let visible = false;
    export const prerender = true;
    export const ssr = true;
	import { onMount } from 'svelte';
	let ready = false;
	onMount(() => {
		ready = true;
        visible = true;
		scrollSlides(1);
	});

	let slideIndex = 1;
	let imageUrl = 'welcome-photo.jpg';
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
		<div class="header">
			<div class="topnav">
                <Hamburger bind:open />
                {#if open}
                    <a href="tel:3306060543" class="header-text fa fa-mobile-phone">&nbsp;(330) 606-0543</a>
                    <a target="_blank" rel="noopener noreferrer" class="header-text" href={infographic}>How To</a>
                {/if}
            </div>
            {#if visible}
                <svg width="100vw" height="50vh" viewBox="0 0 623 396" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <g out:fade={{ duration: 200 }} opacity="1">
                        <path
                            in:expand={{ duration: 10, easing: quintOut }}
                            style="stroke: #6f4930; fill: #56903a; stroke-width: 50;"
                            d={outer}
                        />
                        <path in:draw={{ duration: 11000 }} style="stroke:#FFFFFF; stroke-width: 1.4" d={inner} />
                    </g>
                </svg>

                <div class="centered" out:fly={{ y: -20, duration: 800 }}>
                    {#each 'Explore The River!' as char, i}
                        <span in:fade|global={{ delay: 500 + i * 150, duration: 700 }}>{char}</span>
                    {/each}
                </div>
            {/if}
		</div>
		<div class="about-column">
			<img class="about" src={imageUrl} alt=""/>
			<p>
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
	</div>
</main>
<div class="bottom-info">
	<a href="tel:3306060543" class="fa fa-mobile-phone">&nbsp;&nbsp;&nbsp;(330) 606-0543</a>
	<a href="mailto:kayakron@gmail.com" class="fa fa-envelope">kayakakron@gmail.com</a
	>
</div>

<style scoped>
	:global(body) {
		background-color: #c5b867;
	}

	#phone {
		width: auto;
		text-align: center;
		border-radius: 10px;
		background-color: #495d4e;
		color: #c5b867;
		text-decoration: none;
		font-size: 1em;
	}

	#howto {
		width: auto;
		text-align: center;
		border-radius: 10px;
		background-color: #495d4e;
		color: #c5b867;
		text-decoration: none;
		font-size: 1em;
	}

	.topnav {
		position: absolute;
		top: 0px;
		left: 0;
		width: 95vw;
		font-size: 1.5em;
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
		/* margin: auto; */
        display: flex;
        justify-content: center;
		margin: 0px;
		padding-top: 5vh;
	}

    .dot {visibility: hidden;}

	.slide-image {
		max-height: 100vh;
        height: auto;
	}

    .mySlides {
		display: none;
	}

	/* Next & previous buttons */
	.prev
	{
		cursor: pointer;
		position: absolute;
		top: 50%;
        left: 25%;
		width: auto;
		margin-top: -30vh;
		color: white;
		font-weight: bold;
		font-size: 5em;
		transition: 0.6s ease;
		border-radius: 0 3px 3px 0;
		user-select: none;
	}

	/* Position the "next button" to the right */
	.next {
		cursor: pointer;
		position: absolute;
		top: 50%;
        right: 25%;
		width: auto;
		margin-top: -30vh;
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

	.header-text {
        text-decoration: none;
        color: #333333;
        padding: 2px 6px 2px 6px;
        border-top: 1px solid #CCCCCC;
        border-right: 1px solid #333333;
        border-bottom: 1px solid #333333;
        border-left: 1px solid #CCCCCC;
        float: left;
        justify-content: center;
		background-color: #495d4e;
		font-size: 20px;
		line-height: 25px;
		border-radius: 25px;
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

        .centered-text {
            font-size: 1rem;
            letter-spacing: 0;
        }

        .centered {
            position: absolute;
            left: 50%;
            width: 100vw;
            top: 50%;
            transform: translate(-50%, -50%);
            font-family: 'Cabin Condensed', sans-serif;
            letter-spacing: 0;
            line-height: 0.5;
            color: darkslategrey;
        }
        .centered span {
            will-change: filter;
            font-size: 2rem;
            letter-spacing: 0;
        }
	}

	svg {
		width: 100vw;
		height: auto;
	}

	path {
		fill: #000000;
		opacity: 1;
	}

	label {
		position: absolute;
		top: 1em;
		left: 1em;
	}

	.centered {
		font-size: 5.5em;
		position: absolute;
		left: 50%;
		top: 50%;
		transform: translate(-50%, -50%);
		font-family: 'Overpass';
		letter-spacing: 0.12em;
		color: darkslategrey;
		font-weight: 400;
	}

	.centered span {
		will-change: filter;
	}

</style>
