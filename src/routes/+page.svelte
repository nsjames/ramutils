
<section class="md:flex min-h-full">
	<TabGroup
			justify="justify-center"
			active="variant-filled-primary"
			hover="hover:variant-soft-primary"
			flex="flex-1 lg:flex-none"
			rounded=""
			border=""
			class="md:hidden bg-surface-100-800-token w-full"
	>
		{#each pages as page}
			<TabAnchor href="/" selected={page.index === currentPage} on:click={() => currentPage = page.index}>
				<svelte:fragment slot="lead">
					<i class="fa fas {page.icon}"></i>
				</svelte:fragment>
			</TabAnchor>
		{/each}

		<!-- ... -->
	</TabGroup>
	<AppRail class="hidden md:block">
		{#each pages as page}
			<AppRailTile bind:group={currentPage} value={page.index}>
				<svelte:fragment slot="lead">
					<i class="fa fas {page.icon}"></i>
				</svelte:fragment>
				<span>{page.title}</span>
			</AppRailTile>
		{/each}



	</AppRail>
	<section class="flex-1 mt-2 md:mt-0 mx-2">
		{#if currentPage === 0}
			<Buy />
		{:else if currentPage === 1}
			<Sell />
		{:else if currentPage === 2}
			<Transfer />
		{:else if currentPage === 3}
			<Burn />
		{/if}

	</section>
</section>

<script lang="ts">
	import {AppRail, AppRailAnchor, AppRailTile, Toast, TabGroup, Tab, TabAnchor} from "@skeletonlabs/skeleton";
	import Buy from "../components/Buy.svelte";
	import Sell from "../components/Sell.svelte";
	import Transfer from "../components/Transfer.svelte";
	import Burn from "../components/Burn.svelte";

	const pages = [
		{
			title: "Buy",
			icon: "fa-up",
			index: 0,
		},
		{
			title: "Sell",
			icon: "fa-down",
			index: 1,
		},
		{
			title: "Transfer",
			icon: "fa-exchange",
			index: 2,
		},
			// burn
		{
			title: "Burn",
			icon: "fa-fire",
			index: 3,
		}
	];

	let currentPage: number = 0;

</script>

<style lang="postcss">
	figure {
		@apply flex relative flex-col;
	}
	figure svg,
	.img-bg {
		@apply w-64 h-64 md:w-80 md:h-80;
	}
	.img-bg {
		@apply absolute z-[-1] rounded-full blur-[50px] transition-all;
		animation: pulse 5s cubic-bezier(0, 0, 0, 0.5) infinite,
			glow 5s linear infinite;
	}
	@keyframes glow {
		0% {
			@apply bg-primary-400/50;
		}
		33% {
			@apply bg-secondary-400/50;
		}
		66% {
			@apply bg-tertiary-400/50;
		}
		100% {
			@apply bg-primary-400/50;
		}
	}
	@keyframes pulse {
		50% {
			transform: scale(1.5);
		}
	}
</style>
