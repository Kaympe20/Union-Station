<script lang="ts">
	import { transitModes } from '$lib/utils';
	import { onMount } from 'svelte';
    let isReady = $state(false);
	let { activeTransitMode = "bike" } = $props();
    console.log(activeTransitMode)
	if (!Object.keys(transitModes).includes(activeTransitMode)) {
		console.error('Passed transit mode is not an acceptable value.');
	}
	let Icon: any = $state();
	onMount(async () => {
		Icon = (await import(`$lib/icons/${activeTransitMode}.svelte`)).default;
        isReady = true;
	});
</script>

<div class="h-24 w-64 rounded-lg bg-black">
    {#if isReady}
    <Icon></Icon>
    {/if}
</div>

<style>
</style>
