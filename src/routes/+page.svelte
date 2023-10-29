<script lang="ts">
	import Hamburger from '$lib/Hamburger.svelte';
	import ToggleButton from '$lib/ToggleButton.svelte';

	// defaults
	let isOpen = false;
	let unit = 'rem';
	let width = 6;
	let height = 4;
	let lineHeight = 0.8;
	let lineBorderRadius = 0.4;
	let contain = true;

	function hamburgerClick() {
		isOpen = !isOpen;
	}
</script>

<main>
	<h1>Resizable Animated Hamburger Button Component for Svelte</h1>
	<container>
		<row>
			<div>
				This button does not need to be square, but still will adjust correctly. The implementation
				does not require any depenencies and detects and toggles dark mode.
			</div>
		</row>
		<row>
			<div>Click on the element below to animate</div>
			<div>
				<Hamburger
					{isOpen}
					{hamburgerClick}
					{width}
					{height}
					{lineHeight}
					{unit}
					{contain}
					{lineBorderRadius}
				/>
			</div>
			<div>
				<ToggleButton />
			</div>
		</row>
		<row>
			<form>
				<label for="unit">Unit</label>
				<select id="unit" bind:value={unit}>
					<option value="rem">rem</option>
					<option value="em">em</option>
					<option value="px">pixel</option>
				</select>

				<label for="width">Hamburger Width</label>
				<input id="width" type="number" bind:value={width} min="1" />

				<label for="height">Hamburger Height</label>
				<input id="height" type="number" bind:value={height} min="1" />

				<label for="lineHeight">Line Height</label>
				<input id="lineHeight" type="number" bind:value={lineHeight} min="0" />

				<label for="lineBorderRadius">Line Border Radius</label>
				<input id="lineBorderRadius" type="number" bind:value={lineBorderRadius} min="0" />

				<label for="contain">Fit when open?</label>
				<input id="contain" type="checkbox" bind:checked={contain} min="0" />
			</form>
			{#if lineHeight * 3 > height}
				<div class="warning">
					Warning: Line height exeeds available space and will not display correctly when open!
				</div>
			{/if}
		</row>
	</container>
	<section>
		Checkout the <a href="https://svelte.dev/repl/b43ad27a5d874f9fa84465c9f8fe759b?version=4.2.2"
			>Svelte REPL</a
		>
		or the
		<a href="https://github.com/svenlindstroem/sveltekit-animated-hamburger">Github Repo</a>
	</section>
</main>

<style>
	container {
		display: flex;
		flex-direction: row;
		flex-wrap: wrap;
		& row {
			flex: 1 1 0;
			margin: 1rem;
			& div {
				margin-bottom: 1rem;
			}
		}
		& row:nth-child(2) div {
			text-align: center;
		}
	}

	form {
		display: flex;
		flex-direction: column;
		& label:not(:first-child) {
			margin-top: 1rem;
		}
	}
	.warning {
		color: red;
	}
	section {
		text-align: center;
	}
</style>
