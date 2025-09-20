<script lang="ts">
    const transitModes = {
        car: "Car",
        walk: "Walk",
        bike: "Bike",
        tram: "Tram",
        metroRail: "Metro Rail",
        passengerRail: "Passenger Rail",
        bus: "Bus",
        plane: "Plane",
        transfer: "Transfer"
    }

    let { activeTransitMode } = $props();

    if (!(Object.keys(transitModes).includes(activeTransitMode))) {
        console.error("Passed transit mode is not an acceptable value.");
    }
</script>

<style>
    
</style>

<div>
    
</div>