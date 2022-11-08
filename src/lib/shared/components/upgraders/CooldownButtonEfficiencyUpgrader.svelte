<script lang="ts">
	import NumberDisplay from '$lib/shared/components/displays/NumberDisplay.svelte';

	// upgrade settings
	export let multiplier = 1.07;
	export let baseCost = 5;
	export let benefit = 0.1;
	export let levels = 1;

	// resources
	export let stuff: number;

	// generator settings
	export let msPerTick = 3000;

	let selectedAmount = 1;

	const upgrade = (amount: number) => {
		let finalLevelCost = 0;
		let totalBenefit = 0;
		for (let i = levels, max = levels + amount; i < max; i++) {
			finalLevelCost += baseCost * multiplier ** i;
			totalBenefit += (msPerTick - totalBenefit) * benefit;
		}

		if (stuff < finalLevelCost) throw new Error('Not enough stuff');
		stuff -= finalLevelCost;
		levels += amount;
		msPerTick -= totalBenefit;
	};

	$: getCost = (amount: number) => {
		let finalCost = 0;
		for (let i = levels, max = levels + amount; i < max; i++) {
			finalCost += baseCost * multiplier ** i;
		}
		return finalCost;
	};
</script>

<div class="overflow-hidden rounded-lg bg-white px-4 shadow sm:p-6">
	<dt class="truncate text-sm font-medium text-gray-500">Efficiency Upgrade</dt>
	<span class="isolate inline-flex rounded-md shadow-sm pt-2">
		<button
			type="button"
			class="relative inline-flex items-center rounded-l-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => upgrade(1)}"
			on:mouseenter="{() => (selectedAmount = 1)}">x1</button
		>
		<button
			type="button"
			class="relative -ml-px inline-flex items-center border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => upgrade(10)}"
			on:mouseenter="{() => (selectedAmount = 10)}">x10</button
		>
		<button
			type="button"
			class="relative -ml-px inline-flex items-center rounded-r-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => upgrade(100)}"
			on:mouseenter="{() => (selectedAmount = 100)}">x100</button
		>
	</span>
	<dt class="truncate text-xs font-medium text-gray-500"
		>Cost: <NumberDisplay value="{getCost(selectedAmount)}" /></dt
	>
</div>
