<script lang="ts">
	import NumberDisplay from '$lib/shared/components/displays/NumberDisplay.svelte';

	// upgrade settings
	export let reClickerCost = 0;
	export let autoClickerCost = 0;
	export let reClicker = false;
	export let autoClicker = false;

	// resources
	export let stuff: number;

	const costs = { reClicker: reClickerCost, autoClicker: autoClickerCost };
	let selectedUpgrade: keyof typeof costs = 'reClicker';

	const upgradeReClicker = () => {
		if (stuff < reClickerCost) throw new Error('Not enough stuff');
		if (reClicker) throw new Error('Already Purchased');

		stuff -= reClickerCost;
		reClicker = true;
	};

	const upgradeAutoClicker = () => {
		if (stuff < autoClickerCost) throw new Error('Not enough stuff');
		if (autoClicker) throw new Error('Already Purchased');

		stuff -= autoClickerCost;
		autoClicker = true;
	};

	$: getCost = () => costs[selectedUpgrade];
</script>

<div class="overflow-hidden rounded-lg bg-white px-4 shadow sm:p-6">
	<dt class="truncate text-sm font-medium text-gray-500">Button Upgrades</dt>
	<span class="isolate inline-flex rounded-md shadow-sm pt-2">
		<button
			type="button"
			class="relative inline-flex items-center rounded-l-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => upgradeReClicker()}"
			on:mouseenter="{() => (selectedUpgrade = 'reClicker')}">Auto Button Reset</button
		>
		<button
			type="button"
			class="relative -ml-px inline-flex items-center border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => upgradeAutoClicker()}"
			on:mouseenter="{() => (selectedUpgrade = 'autoClicker')}">Auto Presser</button
		>
	</span>
	<dt class="truncate text-xs font-medium text-gray-500"
		>Cost: <NumberDisplay value="{getCost()}" /></dt
	>
</div>
