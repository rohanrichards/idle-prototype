<script lang="ts">
	let generators = 1;
	let upgrades = 0;
	let stuff = 0;
	let things = 0;
	let stuffPerTick = 0.1;
	const stuffPerThings = 1;
	const generatorBaseCost = 10;
	const generatorCostMultiplier = 1.07;
	let thingsPerGenerator = 10;
	const upgradeBaseCost = 1000;
	const upgradeMultiplier = 1.7;
	let thingsPerUpgrade = 1000;

	const tickInterval = 100;

	const tick = () => {
		stuff += generators * stuffPerTick;
	};

	setInterval(() => {
		tick();
	}, tickInterval);

	const buyGenerators = (count: number) => {
		if (things < thingsPerGenerator * count) throw new Error('Not enough things');
		things -= thingsPerGenerator * count;
		for (let index = 0; index < count; index++) {
			thingsPerGenerator = generatorBaseCost * generatorCostMultiplier ** generators;
			generators += 1;
		}
	};

	const upgradeGenerators = () => {
		if (things < thingsPerUpgrade) throw new Error('Not enough things');
		things -= thingsPerUpgrade;
		upgrades += 1;
		thingsPerUpgrade = upgradeBaseCost * upgradeMultiplier ** upgrades;
		stuffPerTick += 0.01;
	};

	const sellStuff = () => {
		things += stuff * stuffPerThings;
		stuff = 0;
	};
</script>

<dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-3">
	<div class="overflow-hidden rounded-lg bg-white px-4 shadow sm:p-6">
		<dt class="truncate text-sm font-medium text-gray-500">Generators</dt>
		<dd class="mt-1 text-3xl font-semibold tracking-tight text-gray-900">{generators}</dd>
		<dt class="truncate text-sm font-medium text-gray-500"
			>Stuff/Tick: {stuffPerTick.toFixed(2)}</dt
		>
		<dd class="mt-1 text-lg font-semibold tracking-tight text-gray-900">Buy</dd>
		<dt class="truncate text-sm font-medium text-gray-500"
			>Cost: {thingsPerGenerator.toFixed(2)} things</dt
		>
		<span class="isolate inline-flex rounded-md shadow-sm pt-2">
			<button
				type="button"
				class="relative inline-flex items-center rounded-l-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
				on:click="{() => buyGenerators(1)}">+1</button
			>
			<button
				type="button"
				class="relative -ml-px inline-flex items-center border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
				on:click="{() => buyGenerators(5)}">+5</button
			>
			<button
				type="button"
				class="relative -ml-px inline-flex items-center rounded-r-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
				on:click="{() => buyGenerators(10)}">+10</button
			>
		</span>

		<dd class="mt-1 text-lg font-semibold tracking-tight text-gray-900">Upgrade</dd>
		<dt class="truncate text-sm font-medium text-gray-500"
			>Cost: {thingsPerUpgrade.toFixed(2)} things</dt
		>
		<span class="isolate inline-flex rounded-md shadow-sm pt-2">
			<button
				type="button"
				class="relative inline-flex items-center rounded-l-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
				on:click="{() => upgradeGenerators()}">+0.01</button
			>
		</span>
	</div>

	<div class="overflow-hidden rounded-lg bg-white px-4 py-5 shadow sm:p-6">
		<dt class="truncate text-sm font-medium text-gray-500"
			>Stuff ({((generators * stuffPerTick) / (tickInterval / 1000)).toFixed(2)}/s)</dt
		>
		<dd class="mt-1 text-3xl font-semibold tracking-tight text-gray-900">{stuff.toFixed(2)}</dd>
		<button
			type="button"
			class="relative -ml-px inline-flex items-center rounded-r-md border border-gray-300 bg-white px-4 py-2 text-sm font-medium text-gray-700 hover:bg-gray-50 focus:z-10 focus:border-indigo-500 focus:outline-none focus:ring-1 focus:ring-indigo-500"
			on:click="{() => sellStuff()}">Sell Stuff</button
		>
	</div>

	<div class="overflow-hidden rounded-lg bg-white px-4 py-5 shadow sm:p-6">
		<dt class="truncate text-sm font-medium text-gray-500">Things</dt>
		<dd class="mt-1 text-3xl font-semibold tracking-tight text-gray-900">{things.toFixed(2)}</dd
		>
	</div>
</dl>
