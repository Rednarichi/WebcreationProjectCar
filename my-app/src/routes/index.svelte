<script context="module">
	export const prerender = true;
</script>

<script>
	import Video_cars from '/src/lib/car_promo_video.mp4';
	import Home_cars from '/src/lib/lamborghini-aventador-svj.jpg'
	import Test_drive from '/src/lib/test_drive_car.jpg';
	import About_drive from '/src/lib/about_drive.jpg';
</script>

<svelte:head>
	<title>Auto Prestige</title>
	<meta name="description" content="Car dealership" />
</svelte:head>


<section>

	<div class="w-full sm:object-cover sm:object-center bg-gray-900 relative group sm:text-1xl">
		<video class="w-full" src={Video_cars} type="video/mp4" autoplay loop muted  alt="Blue Lamborguini Aventador">
	</div>

	<div class="mt-2 w-full sm:object-cover sm:object-center bg-gray-900 relative group sm:text-1xl">
		<img class="hover:opacity-80 duration-200" src={Home_cars} alt="Blue Lamborguini Aventador">
		<a class="absolute inset-x-2 bottom-6 justify-left items-end font-semibold text-white opacity-75 hover:opacity-100 " href="/models">
			Discover our prestigious models
		</a>	
	</div>

	<div class="mt-2 w-full sm:object-cover sm:object-center bg-gray-900 relative group pd-">
		<img class="hover:opacity-80 duration-200" src={Test_drive} alt="Test Drive">
		<a class="absolute inset-x-100 bottom-6 justify-right items-end font-semibold text-white opacity-75 hover:opacity-100 " href="/test_drive">
			Test our prestigious cars
		</a>	
	</div>

	<div class="mt-2 w-full sm:object-cover sm:object-center bg-gray-900 relative group pd-">
		<img class="hover:opacity-80 duration-200" src={About_drive} alt="About Us">
		<a class="absolute inset-x-100 bottom-6 justify-right items-end font-semibold text-white opacity-75 hover:opacity-100 " href="/about">
			Learn about us
		</a>	
	</div>

</section>

<style>
a {
	font-size: 2.5em;
}
</style>
