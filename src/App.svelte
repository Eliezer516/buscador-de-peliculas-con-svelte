<script>
	export let name;
</script>

<main>
	<div class="bg-white md:rounded-xl w-full h-full p-4">
		<div class="flex justify-center items-center flex-col">
			<h1 class="text-5xl text-center mb-4">Buscador de peliculas</h1>
			<input type="text" class="border border-black rounded outline-none p-2">
		</div>
		<div class="grid grid-cols-4 gap-4">
			<div class="card border-2 border-black rounded-md">
			  <header class="p-2">
			    <h1 class="text-2xl">Avengers infiniti war</h1>
			  </header>
			  <img src="https://fakeimg.pl/300/" alt="hola" class="border-t-2 border-b-2 border-black">
			  <footer class="p-2">
			    <button class="bg-indigo-500 px-4 text-white rounded hover:bg-indigo-400">ver</button>
			  </footer>
			</div>
		</div>
	</div>
</main>

<style>

</style>