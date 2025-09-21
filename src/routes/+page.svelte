<script lang="ts">
	import Bar from '$lib/Bar.svelte';
	import {views} from '$lib/utils'
    import TransitRouteCard from '$lib/TransitRouteCard.svelte';
    import { transitModes } from '$lib/utils'
    let currentView = $state(views.Home)
</script>

<Bar bind:currentView={currentView}/>
<p>
    {currentView}
</p>
<TransitRouteCard activeTransitMode={"bike"} departure={new Date("2025-09-20T07:00:00Z")} arrival={new Date("2025-09-20T08:00:00Z")} cost={123.45}></TransitRouteCard>
