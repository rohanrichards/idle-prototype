<script lang="ts">
	export let value = 0;
	const formatter = Intl.NumberFormat('en', { notation: 'compact', maximumFractionDigits: 2 });

	$: parsedNumber = formatter.format(value);
</script>

{parsedNumber}
