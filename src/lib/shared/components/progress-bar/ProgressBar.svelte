<script lang="ts">
	export let value = 10;
	export let max = 100;

	$: currentPercent = (value / max) * 100;
</script>

<div class="h-3 relative max-w-xl rounded-full overflow-hidden">
	<div class="w-full h-full bg-gray-200 absolute"></div>
	<div class="h-full bg-green-500 absolute" style="width:{currentPercent}%"></div>
</div>
