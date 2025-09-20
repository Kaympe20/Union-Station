<script lang="ts">
	import {views} from '$lib/utils'
	let { currentView = $bindable(), ...props } = $props();
</script>

<div class="flex h-16 w-screen items-center bg-[#442f51ff] p-10">
	<h1 class="text-3xl font-black text-white">Union Station Transit Planner</h1>
	<div class="flex w-[25vw] justify-between font-bold ml-10">
		{#each Object.values(views) as page}
			<button class={page === currentView ? 'rounded-2xl bg-[#6b5780ff] p-3 cursor-pointer' : 'p-3 cursor-pointer'} onclick={() => {currentView = page}}>{page}</button>
		{/each}
	</div>
</div>
