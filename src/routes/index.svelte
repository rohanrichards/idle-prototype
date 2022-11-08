<script lang="ts">
	// Start: External Imports
	// End: External Imports

	// Start: Svelte Imports
	// End: Svelte Imports

	// Start: Local Imports

	// Core services

	// Utils

	// Components
	import HeadTags from '$components/head-tags/HeadTags.svelte';
	import BlogPost from '$components/blog-post/BlogPost.svelte';
	import ProjectCard from '$components/project-card/ProjectCard.svelte';
	import CooldownButtonGenerator from '$lib/shared/components/generators/CooldownButtonGenerator.svelte';
	import CooldownButtonEfficiencyUpgrader from '$lib/shared/components/upgraders/CooldownButtonEfficiencyUpgrader.svelte';
	import CooldownButtonStuffUpgrader from '$lib/shared/components/upgraders/CooldownButtonStuffUpgrader.svelte';
	import NumberDisplay from '$lib/shared/components/displays/NumberDisplay.svelte';

	// Models
	import type { IMetaTagProperties } from '$models/interfaces/imeta-tag-properties.interface';
	import type { IProjectCard } from '$models/interfaces/iproject-card.interface';
	import type { IBlogPostSummary } from '$models/interfaces/iblog-post-summary.interface';
	import ExternalLink from '$ui/components/external-link/ExternalLink.svelte';
	import CooldownButtonClickerUpgrader from '$lib/shared/components/upgraders/CooldownButtonClickerUpgrader.svelte';
	import Error from './__error.svelte';
	// End: Local Imports

	// Exports
	// Start: Local component properties
	const metaData: Partial<IMetaTagProperties> = {
		title: `Sveltekit Start | Sveltekit`,
		description:
			'Sveltekit starter project created with sveltekit, typescript, tailwindcss, postcss, husky, and storybook. The project has the structure set up for the scaleable project. (sveltekit, typescript, tailwindcss, postcss, husky, Storybook).',
		keywords: ['sveltekit', 'sveltekit starter', 'sveltekit starter home'],
	};

	const buttonSettings = {
		baseStuffPerTick: 1,
		stuffPerTick: 1,
		baseMsPerTick: 3000,
		msPerTick: 3000,
		reClicker: false,
		autoClicker: false,
	};

	const buttunUpgradeSettings = {
		efficiency: {
			multiplier: 1.07,
			baseCost: 5,
			benefit: 0.05,
			levels: 0,
		},
		stuff: {
			multiplier: 1.07,
			baseCost: 10,
			benefit: 1,
			levels: 0,
		},
		clicks: {
			reClickerCost: 100,
			autoClickerCost: 1000,
		},
	};

	const resources = {
		stuff: 1000,
	};
</script>

<!-- Start: Header Tag -->
<HeadTags metaData="{metaData}" />
<!-- End: Header Tag -->

<!-- Start: Home Page container -->
Stuff: <NumberDisplay value="{resources.stuff}" />
<dl class="mt-5 grid grid-cols-1 gap-5 sm:grid-cols-4">
	<CooldownButtonGenerator
		stuffPerTick="{buttonSettings.stuffPerTick}"
		msPerTick="{buttonSettings.msPerTick}"
		bind:stuff="{resources.stuff}"
		reClicker="{buttonSettings.reClicker}"
		autoClicker="{buttonSettings.autoClicker}"
	/>

	<CooldownButtonEfficiencyUpgrader
		multiplier="{buttunUpgradeSettings.efficiency.multiplier}"
		baseCost="{buttunUpgradeSettings.efficiency.baseCost}"
		benefit="{buttunUpgradeSettings.efficiency.benefit}"
		bind:levels="{buttunUpgradeSettings.efficiency.levels}"
		bind:stuff="{resources.stuff}"
		bind:msPerTick="{buttonSettings.msPerTick}"
	/>

	<CooldownButtonStuffUpgrader
		multiplier="{buttunUpgradeSettings.stuff.multiplier}"
		baseCost="{buttunUpgradeSettings.stuff.baseCost}"
		benefit="{buttunUpgradeSettings.stuff.benefit}"
		bind:levels="{buttunUpgradeSettings.stuff.levels}"
		bind:stuff="{resources.stuff}"
		bind:stuffPerTick="{buttonSettings.stuffPerTick}"
	/>

	<CooldownButtonClickerUpgrader
		bind:stuff="{resources.stuff}"
		reClickerCost="{buttunUpgradeSettings.clicks.reClickerCost}"
		autoClickerCost="{buttunUpgradeSettings.clicks.autoClickerCost}"
		bind:reClicker="{buttonSettings.reClicker}"
		bind:autoClicker="{buttonSettings.autoClicker}"
	/>
</dl>

<!-- End: Home Page container -->
