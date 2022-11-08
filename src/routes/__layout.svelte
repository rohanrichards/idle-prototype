<script lang="ts">
	// Start: Local Imports

	// Start: External Imports
	import '../styles/tailwind.css';

	// End: External Imports

	// Core services

	// Components
	import Header from '$ui/components/headers/Header.svelte';
	import Footer from '$ui/components/footers/Footer.svelte';
	// End: Local Imports

	// Start: Local component properties

	// End: Local component properties

	// Start: Local component methods

	const toggleThemeMode = (event: CustomEvent<{ dark: boolean }>): void => {
		const htmlTag = document.getElementsByTagName('html').item(0);
		if (htmlTag) {
			htmlTag.className = event.detail.dark ? 'dark' : 'light';
		}
	};

	// End: Local component methods
</script>

<div class="bg-white dark:bg-black min-w-full max-w-full min-h-full max-h-full">
	<!-- Start: Header Navigation -->
	<Header on:toggleTheme="{(e) => toggleThemeMode(e)}" useThemeModeButton="{true}" />
	<!-- End: Header Navigation -->
	<main
		class="flex flex-col w-full bg-white dark:bg-black min-w-full min-h-full max-h-full justify-center items-center"
	>
		<div class="divide-y divide-gray-200 overflow-hidden rounded-lg bg-white shadow w-8/12">
			<div class="px-4 py-5 sm:px-6">
				<h3 class="text-lg font-medium leading-6 text-gray-900">Idle Prototype</h3>
			</div>
			<div class="px-4 py-5 sm:p-6">
				<!-- Content goes here -->
				<slot />
			</div>
		</div>
	</main>
</div>
