<script lang="ts">
	import SveltyPicker from 'svelty-picker';
	import { transitModes } from '$lib/utils';

	let departureTimeOutput = $state(new Date('2025-09-20T07:00:00Z').toISOString());
	let departureTime = $derived(() => new Date(departureTimeOutput));
	let arrivalTimeOutput = $state(new Date('2025-09-20T07:00:00Z').toISOString());
	let arrivalTime = $derived(() => new Date(arrivalTimeOutput));

	let costOutput: string = $state('');
	let cost = $derived(() => parseFloat(costOutput));

	let selectedTransitMode = $state('');

	$effect(() => {
		console.log('Departure Time:', departureTimeOutput);
		console.log('Arrival Time:', arrivalTimeOutput);
		console.log('Cost:', costOutput);
		console.log('Selected Transit Mode:', selectedTransitMode);
	});

	function save() {
		const segment = {
			departureTime: departureTime(),
			arrivalTime: arrivalTime(),
			cost: cost(),
			transitMode: selectedTransitMode
		};

		if (!document.cookie) {
			document.cookie = `trips=[{"segments":[${JSON.stringify(segment)}]}]`;
		} else {
			let existingTrips = JSON.parse(document.cookie.split('=')[1]);
			existingTrips[0].segments.push(segment);
			document.cookie = `trips=${JSON.stringify(existingTrips)}`;
		}

		console.log('Segment saved:', segment);
	}
</script>

<div
	class="flex h-auto w-200 flex-col items-center gap-10 rounded-2xl border-1 border-black bg-[#473a54] p-5 text-center"
>
	<div>
		<p class="mb-2 text-2xl font-bold">Departure</p>
		<div class="flex gap-5">
			<SveltyPicker
				mode="datetime"
				format="yyyy-mm-ddThh:mm:ssZ"
				bind:value={departureTimeOutput}
				pickerOnly={true}
			/>
		</div>
	</div>
	<div>
		<p class="mb-2 text-2xl font-bold">Arrival</p>
		<div class="flex gap-5">
			<SveltyPicker
				mode="datetime"
				format="yyyy-mm-ddThh:mm:ssZ"
				bind:value={arrivalTimeOutput}
				pickerOnly={true}
			/>
		</div>
	</div>
	<div class="flex justify-between gap-3">
		<div class="flex-1">
			<p class="mb-2 text-2xl font-bold">Cost</p>
			<input
				type="text"
				bind:value={costOutput}
				class="h-12 w-full rounded-md border-2 border-gray-300 p-2"
			/>
		</div>
		<div class="flex-1">
			<p class="mb-2 text-2xl font-bold">Transit Mode</p>
			<select
				bind:value={selectedTransitMode}
				class="h-12 w-full rounded-md border-2 border-gray-300 p-2"
			>
				{#each Object.keys(transitModes) as mode}
					<option value={mode}>{transitModes[mode as keyof typeof transitModes]}</option>
				{/each}
			</select>
		</div>
	</div>

	<button
		class="cursor-pointer rounded-2xl bg-[#6b5780ff] px-4 py-2 font-bold text-white hover:bg-[#5a4670ff]"
		onclick={save}>Save</button
	>
</div>
