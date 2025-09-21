<script lang="ts">
    import { views } from '$lib/utils';
    import TransitRouteCard from '$lib/TransitRouteCard.svelte';
    import { transitModes } from '$lib/utils';
    import Home from '$lib/views/Home.svelte';
    import About from '$lib/views/About.svelte';
    import MyTrips from '$lib/views/MyTrips.svelte';
    import Plan from '$lib/views/Plan.svelte';

    let currentView = $state("Home");

</script>

<div class="flex h-16 w-screen items-center bg-[#442f51ff] p-10">
	<h1 class="text-3xl font-black text-white">Union Station Transit Planner</h1>
	<div class="flex w-[25vw] justify-between font-bold ml-10">
		{#each Object.values(views) as page}
			<button class={page === currentView ? 'rounded-2xl bg-[#6b5780ff] p-3 cursor-pointer' : 'p-3 cursor-pointer'} onclick={() => {currentView = page}}>{page}</button>
		{/each}
	</div>
</div>

<div class="p-4">
    {#if currentView === "Home"}
    <Home></Home>
    {:else if currentView === "About"}
    <About></About>
    {:else if currentView === "My Trips"}
    <MyTrips></MyTrips>
    {:else if currentView === "Plan a Trip"}
    <Plan></Plan>
    {/if}
</div>