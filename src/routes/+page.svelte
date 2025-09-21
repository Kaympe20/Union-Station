<script lang="ts">
    import Bar from '$lib/Bar.svelte';
    import { views } from '$lib/utils';
    import TransitRouteCard from '$lib/TransitRouteCard.svelte';
    import { transitModes } from '$lib/utils';
    import Home from '$lib/views/Home.svelte';
    import About from '$lib/views/About.svelte';
    import MyTrips from '$lib/views/MyTrips.svelte';
    import Plan from '$lib/views/Plan.svelte';

    let currentView = $state("Home");
</script>

<Bar bind:currentView={currentView} />

<div class="p-4">
    {#if currentView === "Home"}
    <Home></Home>
    {:else if currentView === "About"}
    <About></About>
    {:else if currentView === "MyTrips"}
    <MyTrips></MyTrips>
    {:else if currentView === "Plan"}
    <Plan></Plan>
    {/if}
</div>
