<script lang="ts">
	import NumberDisplay from '$lib/shared/components/displays/NumberDisplay.svelte';
	import ProgressBar from '../progress-bar/ProgressBar.svelte';

	export let stuff: number;
	export let stuffPerTick = 1;
	export let msPerTick = 3000;
	export let reClicker = false;
	export let autoClicker = false;

	let cooldownTime = msPerTick;
	let active = false;
	let generatorTimer: ReturnType<typeof setInterval>;
	const updateIntervalMs = 10;
	let mouseDown = false;
	let buttonState = 'ready';

	const clickHandler = () => {
		if (!active) {
			active = true;
			clearInterval(generatorTimer);
			cooldownTime = msPerTick;
			generatorTimer = setInterval(() => {
				if (active) {
					cooldownTime -= updateIntervalMs;
					if (cooldownTime <= 0) {
						tickHandler(); // <--- USED BEFORE DEFINED
					}
					if (autoClicker) {
						clickHandler();
					}
				}
			}, updateIntervalMs);
		}
	};

	const tickHandler = () => {
		stuff += stuffPerTick;
		clearInterval(generatorTimer);
		active = false;
		cooldownTime = msPerTick;

		if (mouseDown && reClicker) {
			clickHandler();
		}
	};

	$: {
		if (!active && mouseDown) {
			buttonState = 'error';
		} else {
			buttonState = 'ok';
		}
	}
</script>

<div class="overflow-hidden rounded-lg bg-white px-4 shadow sm:p-6">
	<dt class="truncate text-sm font-medium text-gray-500">The Button</dt>
	<button
		type="button"
		on:mousedown="{() => {
			mouseDown = true;
			clickHandler();
		}}"
		on:mouseup="{() => {
			mouseDown = false;
		}}"
		class="inline-flex items-center rounded-md border border-transparent 
			{buttonState === 'ok' ? 'bg-indigo-600 hover:bg-indigo-700' : 'bg-red-600 hover:bg-red-700'} 			
			px-6 py-3 text-base font-medium text-white shadow-sm  focus:outline-none "
		>{buttonState === 'ok' ? 'Push Me' : 'Release Me'}</button
	>
	Stuff: <NumberDisplay value="{stuffPerTick}" />
	<ProgressBar value="{cooldownTime}" max="{msPerTick}" />
</div>
