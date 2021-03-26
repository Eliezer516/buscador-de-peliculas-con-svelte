<script>
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
	<div class="bg-white md:rounded-xl w-full h-full p-4">
		<div class="flex flex-col mb-4">
			<h1 class="text-5xl mb-4">Buscador de peliculas</h1>
			<div class="flex">
				<input type="text" {value} on:input={inputescrito} class="border border-black rounded outline-none text-2xl mr-4 p-2">
				{#if cargado}
					<h3 class="text-3xl">Obteniendo datos...</h3>
				{/if}
			</div>


		</div>
		<div class="grid grid-cols-4 gap-4" id="cards">
			{#if respuesta.length > 0}
			{#each respuesta as {Title, Year, Poster, Type}}
			  <div class="rounded overflow-hidden shadow-lg">
			    <img class="w-full" src={Poster} alt={Title}>
			    <div class="px-6 py-4">
			      <div class="font-bold text-xl mb-2">{Title}</div>
			      <p class="text-gray-700 text-base">
			      	{Year}
			      </p>
			    </div>
			    <div class="px-6 pt-4 pb-2">
			      <span class="inline-block bg-gray-200 rounded-full px-3 py-1 text-sm font-semibold text-gray-700 mr-2 mb-2">{Type}</span>
			    </div>
			  </div>
			{/each}
			{/if}
			<template id="template-card">
				<div class="card border-2 border-black rounded-md">
					<header class="p-2 text-2xl">
					</header>
					<img src="https://fakeimg.pl/300/" alt="hola" class="border-t-2 border-b-2 border-black">
					<footer class="p-2">
					</footer>
				</div>
			</template>
		</div>
	</div>
</main>

<style>

</style>