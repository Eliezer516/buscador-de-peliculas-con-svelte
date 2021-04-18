<script>
	import AOS from 'aos';
	import 'aos/dist/aos.css';

	AOS.init();

	let value = '';
	let respuesta = []
	let cargado = false

	const inputescrito = e => value = e.target.value

	$: if (value.length > 2) {
		cargado = true
		fetch(`https://www.omdbapi.com/?s=${value}&apikey=422350ff`)
		.then(res => res.json())
		.then(data => {
			respuesta = data.Search || []
			console.log(data)
			cargado = false
		})
	}
</script>

<main>
	<div class="bg-white md:rounded-xl p-5">
		<div class="flex pb-8 mb-8 border-b border-black relative flex-col md:flex-row">
			<h1 class="text-5xl md:mr-4 text-center">Buscador de peliculas</h1>
			<div class="flex flex-col md:flex-row md:ml-8 mt-8 md:mt-0">
				<input type="text" {value} on:input={inputescrito} class="border border-black rounded outline-none text-2xl px-2">
				{#if cargado}
				<div class="loader relative p-8" data-aos="fade">
					<span></span>
					<span></span>
					<span></span>
				</div>
				{/if}
			</div>
		</div>
		<div class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-4 gap-4" id="cards">
			{#if respuesta.length > 0}
			{#each respuesta as {Title, Year, Poster, Type}}
			  <div class="rounded overflow-hidden shadow-lg" data-aos="fade-up">
			  	{#if Poster === "N/A"}
			    	<img class="w-full" src="notfound.png" alt={Title}>
			    {:else}
			    	<img class="w-full" src={Poster} alt={Title}>
			  	{/if}
			    <div class="px-6 py-4">
			      <div class="font-bold text-xl mb-2">{Title}</div>
			      <p class="text-gray-700 text-lg">
			      	Año: {Year}
			      </p>
			    </div>
			    <div class="px-6 pb-2">
			      <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{Type}</span>
			    </div>
			  </div>
			{/each}
			{/if}
		</div>
	</div>
</main>

<style>
	.loader span:nth-child(1){
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 30px;
		height: 30px;
		border: 3px solid black;
		border-radius: 50%;
		border-top: 3px solid transparent;
		animation: animate 1s linear infinite;
	}
	.loader span:nth-child(2){
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 50px;
		height: 50px;
		border: 3px solid black;
		border-radius: 50%;
		border-bottom: 3px solid transparent;
		animation: animate 2s linear infinite;
	}
	.loader span:nth-child(3){
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%);
		width: 10px;
		height: 10px;
		border: 3px solid black;
		border-radius: 50%;
		border-bottom: 3px solid transparent;
		animation: animate 1s linear infinite;
	}

	@keyframes animate{
		0%{
			transform: translate(-50%, -50%) rotate(0deg);
		}
		100%{
			transform: translate(-50%, -50%) rotate(360deg);
		}
	}
</style>