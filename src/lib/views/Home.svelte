<script lang="ts">
    import { browser } from "$app/environment";
    import NewSegmentModal from "$lib/newSegmentModal.svelte";
    import TransitRouteCard from "$lib/TransitRouteCard.svelte";

    let getStartedClicked = $state(false);

    let newTripName = $state("");

    type TripSegment = {
        transitMode: string;
        departure: string | Date;
        arrival: string | Date;
        cost: number;
    };

    let newTripSegments = $state<TripSegment[]>([]);

    let cookieCache = $derived(
        () => `{
            "name": "${newTripName}",
            "segments": "${newTripSegments}"
        }`  
    );
</script>

<div>
    {#if browser && !document.cookie.includes('trips=') && !getStartedClicked}
        <div class="flex min-h-screen flex-col gap-3 items-center justify-center p-10">
            <h1 class="text-3xl font-extrabold text-white">Welcome! It doesn't look like you've added any trips yet.</h1>
            <button class="cursor-pointer rounded-2xl bg-[#6b5780ff] px-4 py-2 font-bold text-white hover:bg-[#2e1e3f] duration-450" onclick={() => getStartedClicked = true}>Get Started!</button>
        </div>
    {:else}
        <div class="text-center w-[90%] mx-auto">
            <h1 class="text-4xl font-extrabold text-white mb-5">New Trip</h1>
            <input type="text" bind:value={newTripName} class="h-12 w-full rounded-md border-2 border-gray-300 p-2" placeholder="Trip Name"/>
            <div class="auto-cols-auto table-auto">
                {#each newTripSegments as segment, index}
                    <TransitRouteCard 
                        activeTransitMode={segment.transitMode} 
                        departure={new Date(segment.departure)} 
                        arrival={new Date(segment.arrival)} 
                        cost={segment.cost} 
                    />
                {/each}
            </div>
        </div>
        
    {/if}
    
</div>