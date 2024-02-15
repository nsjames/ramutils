<section class="flex min-h-full w-full items-center justify-center">
    <section class="min-w-full md:min-w-[400px] card variant-glass md:p-8 p-4">

        <h1 class="h1">Login</h1>
        <p class="text-xs mt-3 mb-10">
            Before you can do anything here, you need to log in.
        </p>

        <button class="btn variant-filled-primary w-full h-16" on:click={ChainService.login}>
            <i class="fa fa fa-right-to-bracket"></i>
            <span class="ml-2 font-black">Login</span>
        </button>


    </section>

</section>

<script lang="ts">
    import Spacer from "./Spacer.svelte";
    import ChainService, {account, accountBytes} from "../services/chain.service";

</script>