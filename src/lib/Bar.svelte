<script lang="ts">
	const views = {
		Home: "Home",
		About: "About",
		MyTrips: "My Trips",
		Plan: "Plan a Trip"
	};
	let currentView = $state(views.Home);
</script>

<div class="flex h-16 w-screen items-center bg-[#442f51ff] p-10">
	<h1 class="text-3xl font-black text-white">Union Station Transit Planner</h1>
	<div class="flex w-[25vw] justify-between font-bold">
		{#each Object.keys(views) as page}
			<button class={page === currentView ? 'rounded-2xl bg-[#6b5780ff] p-3' : ''}
				>{page}</button
			>
		{/each}
	</div>
</div>
