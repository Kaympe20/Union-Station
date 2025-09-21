<script lang="ts">
    import SveltyPicker from 'svelty-picker';
    import { transitModes } from '$lib/utils';

    let departureTime = $state(new Date("2025-09-20T07:00:00Z").toISOString());
    let arrivalTime = $state(new Date("2025-09-20T07:00:00Z").toISOString());

    let cost: Number = $state(0);
</script>

<div class="bg-[#473a54] border-1 border-black w-200 h-auto rounded-2xl flex items-center flex-col gap-10 p-5 text-center">
    <div>
        <p class="mb-2 text-2xl font-bold">Departure</p>
        <div class="flex gap-5">
            <SveltyPicker mode="date" bind:value={departureTime} pickerOnly={true} />
            <SveltyPicker mode="time" bind:value={departureTime} pickerOnly={true} />
        </div>
    </div>
    <div>
        <p class="mb-2 text-2xl font-bold ">Arrival</p>
        <div class="flex gap-5">
            <SveltyPicker mode="date" bind:value={arrivalTime} pickerOnly={true} />
            <SveltyPicker mode="time" bind:value={arrivalTime} pickerOnly={true} />
        </div>
    </div>
    <div class="flex gap-3 justify-between">
        <div class="flex-1">
            <p class="mb-2 text-2xl font-bold ">Cost</p>
            <input type="text" bind:value={cost} class="border-2 border-gray-300 rounded-md p-2 w-full h-12" />
        </div>
        <div class="flex-1">
            <p class="mb-2 text-2xl font-bold ">Transit Mode</p>
            <select class="border-2 border-gray-300 rounded-md p-2 w-full h-12">
                {#each Object.keys(transitModes) as mode}
                    <option value={mode}>{transitModes[mode as keyof typeof transitModes]}</option>
                {/each}
            </select>
        </div>
    </div>
</div>