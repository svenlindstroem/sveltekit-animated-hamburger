<script lang="ts">
	import type { MouseEventHandler } from 'svelte/elements';
	export let isOpen: boolean;
	export let hamburgerClick: MouseEventHandler<HTMLDivElement>;
	export let unit: string = 'rem';
	export let width: number = 6;
	export let height: number = 4;
	export let lineHeight: number = 0.8;
	export let contain: boolean = false;
	export let lineBorderRadius: number = 0.4;

	// vertical line offset when isOpen === true
	$: offset = height / 2 - lineHeight / 2;
</script>

<!-- svelte-ignore a11y-click-events-have-key-events -->
<!-- svelte-ignore a11y-no-static-element-interactions -->
<div
	on:click={hamburgerClick}
	class="h"
	class:isOpen
	style:width={width + unit}
	style:height={height + unit}
>
	<div
		class="l"
		style:height={lineHeight + unit}
		style:transform={isOpen ? `translate(0, ${offset}${unit}) rotate(45deg)` : ''}
		style:width={isOpen && contain
			? Math.sqrt(2 * Math.pow(width > height ? height : width, 2)) - lineHeight + unit
			: width + unit}
		style:border-radius={lineBorderRadius + unit}
	/>
	<div class="l" style:height={lineHeight + unit} style:border-radius={lineBorderRadius + unit} />
	<div
		class="l"
		style:height={lineHeight + unit}
		style:transform={isOpen ? `translate(0, -${offset}${unit}) rotate(-45deg)` : ''}
		style:width={isOpen && contain
			? Math.sqrt(2 * Math.pow(width > height ? height : width, 2)) - lineHeight + unit
			: width + unit}
		style:border-radius={lineBorderRadius + unit}
	/>
</div>

<style>
	div {
		margin: 0 auto;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: center;
		transition: 1s ease-in-out;
		background-color: var(--bg-hamburger);
		& div {
			width: 100%;
			transform: rotate(0deg);
			transform-origin: center;
			background-color: var(--bg-line);
		}
	}

	.isOpen div:nth-child(2) {
		opacity: 0;
	}
</style>
