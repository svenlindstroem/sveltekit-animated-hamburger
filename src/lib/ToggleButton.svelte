<script lang="ts">
	import { onMount } from 'svelte';

	let darkMode = false;
	onMount(() => {
		// on load check what is the current mode
		// in svelte kit windows is only available after mount
		if (window.matchMedia('(prefers-color-scheme: dark)').matches) {
			darkMode = true;
		}

		// attach an event listener
		// listen to changes and set darkMode only when not userdefined
		window.matchMedia('(prefers-color-scheme: dark)').addEventListener('change', (e) => {
			darkMode = e.matches && !document.documentElement.hasAttribute('data-theme') ? true : false;
		});
	});

	function toggle() {
		//document.documentElement.removeAttribute('data-theme');
		const mode = darkMode ? 'light' : 'dark';
		document.documentElement.setAttribute('data-theme', mode);
		darkMode = !darkMode;
	}
</script>

<button on:click={toggle}>
	{#if darkMode}
		Go light
	{:else}
		Go dark
	{/if}
</button>

<style>
	button {
		background: var(--bg-color);
		border: 1px solid var(--text-color);
		border-radius: 5px;
		color: var(--text-color);
		padding: 10px 15px;
	}

	button:active {
		background: inherit;
	}
</style>
