<script lang="ts">
	import TransitRouteCard from "$lib/TransitRouteCard.svelte";
    import { browser } from '$app/environment';

    let cookie = $state('')
    let parsedCookie: any = $derived(() => {
        console.log('Full cookie string:', cookie);
        
        if (!cookie.includes('trips=')) {
            console.error('No trips cookie found.');
            return [];
        }
        
        try {
            const tripsData = cookie.split('trips=')[1].split(';')[0];
            console.log('Trips data from cookie:', tripsData);
            
            const parsed = JSON.parse(decodeURIComponent(tripsData));
            console.log('Parsed trips:', parsed);
            
            return parsed;
        } catch (error) {
            console.error('Error parsing trips cookie:', error);
            return [];
        }
    });

    // Update cookie reactively
    if (browser) {
        cookie = document.cookie;
        
        // Set up an interval to check for cookie changes
        const interval = setInterval(() => {
            const newCookie = document.cookie;
            if (newCookie !== cookie) {
                cookie = newCookie;
            }
        }, 1000);
        
        // Cleanup interval (in a real app, you'd do this in onDestroy)
        // clearInterval(interval);
    }
</script>

<div>
    <h2>My Trips</h2>
    
    <!-- Debug info -->
    <details>
        <summary>Debug Info</summary>
        <p>Cookie: {cookie}</p>
        <p>Parsed trips count: {parsedCookie?.length || 0}</p>
        <pre>{JSON.stringify(parsedCookie, null, 2)}</pre>
    </details>
    
    {#if parsedCookie && parsedCookie.length > 0}
        {#each parsedCookie as trip}
            <TransitRouteCard 
                activeTransitMode={trip.segments[0].transitMode} 
                departure={new Date(trip.segments[0].departure)} 
                arrival={new Date(trip.segments[0].arrival)} 
                cost={trip.segments[0].cost}
            />
        {/each}
    {:else}
        <p>No trips found. Make sure you have saved some trips!</p>
        
        <!-- Button to set test cookie for debugging -->
        <button onclick={() => {
            document.cookie = 'trips=' + encodeURIComponent('[{"name":"f","segments":[{"departure":"2025-12-17T07:12:00.000Z","arrival":"2025-12-31T07:12:00.000Z","cost":1,"transitMode":"car"}]}]') + '; path=/';
            cookie = document.cookie;
        }}>
            Set Test Cookie
        </button>
    {/if}
</div>