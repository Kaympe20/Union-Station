<script lang="ts">
	import { transitModes } from '$lib/utils';
	import { onMount } from 'svelte';

	let isReady = $state(false);

	let { activeTransitMode, departure, arrival, cost } = $props();

	let duration: number = $state(0);

	console.log(activeTransitMode);

	if (!Object.keys(transitModes).includes(activeTransitMode)) {
		console.error('Passed transit mode is not an acceptable value.');
	}

	let Icon: any = $state();

	onMount(async () => {
		Icon = (await import(`$lib/icons/${activeTransitMode}.svelte`)).default;
		isReady = true;
		duration = (arrival - departure) / 1000;
		departure =
			String(departure.getUTCHours()).padStart(2, '0') +
			':' +
			String(departure.getUTCMinutes()).padStart(2, '0');
		arrival =
			String(arrival.getUTCHours()).padStart(2, '0') +
			':' +
			String(arrival.getUTCMinutes()).padStart(2, '0');
	});
</script>

<div class="h-32 w-64 rounded-lg bg-white">
	{#if isReady}
		<div class="flex h-full w-full items-center">
			<div class="m-2 flex h-18 w-18 items-center justify-evenly rounded-full bg-purple-600">
				<div class="h-10 w-10">
					<Icon />
				</div>
			</div>
			<div class="w-34 text-center text-sm font-bold text-black">
				<h1>Departure: {departure}</h1>
				<h1>
					Duration: {String(duration / 60 / 60).padStart(2, '0')}:{String(
						duration % (60 * 60)
					).padStart(2, '0')}
				</h1>
				<h1>Arrival: {arrival}</h1>
				<br />
				<h1>Cost: ${cost}</h1>
			</div>
		</div>
	{:else}
		<p>Wait for the damn icon you useless idiot!</p>
	{/if}
</div>

<style>
</style>
