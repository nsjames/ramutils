

<Toast />

<AppShell>
	<svelte:fragment slot="header">
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-xl uppercase">
					<i class="fa fas fa-ram"></i> RAM
				</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-soft hidden md:block"
					href="https://eosnetwork.com"
					target="_blank"
					rel="noreferrer"
				>
					EOS Network
				</a>
				<a
						class="btn btn-sm variant-soft hidden md:block"
						href="https://t.me/EOS_Global"
						target="_blank"
						rel="noreferrer"
				>
					Telegram
				</a>
				<a
					class="btn btn-sm variant-soft hidden md:block"
					href="https://github.com/eosnetworkfoundation/"
					target="_blank"
					rel="noreferrer"
				>
					GitHub
				</a>


				{#if $account}
					<button class="btn btn-sm variant-filled" on:click={ChainService.logout}>
						Logout
					</button>

				{:else}
					<button class="btn btn-sm variant-filled" on:click={ChainService.login}>
						Login
					</button>

				{/if}


				<LightSwitch />

			</svelte:fragment>
		</AppBar>
	</svelte:fragment>

	<slot />

	<figure class="bg"></figure>
</AppShell>

<script lang="ts">
	import '../app.postcss';
	import { AppShell, AppBar, Toast, initializeStores } from '@skeletonlabs/skeleton';
	import { LightSwitch } from '@skeletonlabs/skeleton';
	import {onMount} from "svelte";
	import ChainService, {account} from "../services/chain.service";
	initializeStores();

	onMount(async () => {
		await ChainService.init();
	})
</script>

<style>
	.bg {
		position: fixed;
		top: 0;
		left: 0;
		width: 100%;
		height: 100%;
		background-image: url('https://source.unsplash.com/random/900×700/?pattern,abstract,texture,geometric,dark');
		background-size: cover;
		background-position: center;
		pointer-events: none;
		z-index: -1;
		filter: blur(40px);
		opacity: 0.15;
	}
</style>

