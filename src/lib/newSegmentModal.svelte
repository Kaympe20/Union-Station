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
    
    let nodeRef: HTMLElement;

    let missingItems = $state(false);

	let { segment = $bindable(), formDoneCallback, ...props } = $props();

	$effect(() => {
		console.log('Departure Time:', departureTimeOutput);
		console.log('Arrival Time:', arrivalTimeOutput);
		console.log('Cost:', costOutput);
		console.log('Selected Transit Mode:', selectedTransitMode);
	});

	function save() {
        if (!departureTimeOutput || !arrivalTimeOutput || !costOutput || !selectedTransitMode) {
            missingItems = true;
            return;
        } else {
            missingItems = false;
        }
        segment = {
            departure: departureTime(),
            arrival: arrivalTime(),
            cost: cost(),
            transitMode: selectedTransitMode
        };

        console.log('Segment saved:', segment);
        formDoneCallback();
    }
</script>

<div
	class="flex h-auto w-200 md:w-full flex-col items-center gap-10 rounded-2xl border-1 border-black p-5 text-center z-99 relative"
    bind:this={nodeRef}
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

    {#if missingItems}
        <p class="text-red-500">Please fill in all fields before saving.</p>
    {/if}

	<button
		class="cursor-pointer rounded-2xl bg-[#6b5780ff] px-4 py-2 font-bold text-white hover:bg-[#5a4670ff]"
		onclick={save}>Save</button>
</div>
