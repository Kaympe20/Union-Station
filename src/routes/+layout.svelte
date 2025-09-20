<script lang="ts">
	import '../app.css';
	import favicon from '$lib/assets/favicon.svg';

	let { children } = $props();
	import { pwaInfo } from 'virtual:pwa-info'; 
	import { onMount } from 'svelte';
  // @ts-ignore
	import { registerSW } from 'virtual:pwa-register';

	onMount(async () => {
    if (pwaInfo) {
      registerSW({
        immediate: true,
        // @ts-ignore
        onRegistered(r) {
          // uncomment following code if you want check for updates
          r && setInterval(() => {
             console.log('Checking for sw update')
             r.update()
          }, 2000 /* 2s for testing purposes */)
          console.log(`SW Registered: ${r}`)
        },
        // @ts-ignore
        onRegisterError(error) {
          console.log('SW registration error', error)
        }
      })
    }
  })

  	let webManifestLink = $derived(pwaInfo ? pwaInfo.webManifest.linkTag : '') 
</script>

<svelte:head>
	{@html webManifestLink}
	<link rel="icon" href={favicon} />
</svelte:head>

{@render children?.()}

{#await import('$lib/ReloadPrompt.svelte') then { default: ReloadPrompt}}
  <ReloadPrompt />
{/await}