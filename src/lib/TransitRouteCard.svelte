<script lang="ts">
	import { onMount, type Component } from "svelte";

    const transitModes = {
        car: "Car",
        walk: "Walk",
        bike: "Bike",
        tram: "Tram",
        metroRail: "Metro Rail",
        passengerRail: "Passenger Rail",
        bus: "Bus",
        plane: "Plane",
        transfer: "Transfer",
        unknown: "Unknown"
    }

    let { activeTransitMode } = $props();

    if (!(Object.keys(transitModes).includes(activeTransitMode))) {
        console.error("Passed transit mode is not an acceptable value.");
    }
    let Icon: any = $state();
    onMount(async() => { Icon = (await import(`/icons/${activeTransitMode}.svelte`)).default;})
</script>

<div class="rounded-lg bg-white w-64 h-24">
    <Icon/>
</div>

<style>
</style>
