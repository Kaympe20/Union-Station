<script lang="ts">
	import Bar from '$lib/Bar.svelte';
	import {views} from '$lib/utils'
    let currentView = $state(views.Home)
</script>

<Bar bind:currentView={currentView}/>
<p>
    {currentView}
</p>