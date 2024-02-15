<section class="flex min-h-full w-full items-center justify-center">
    <!-- glass bg -->
    <section class="py-20 min-w-full md:min-w-[400px] card variant-glass md:p-8 p-4">

        <h1 class="h1">Burn RAM</h1>
        <p class="text-xs mt-3 mb-10">
            Burn RAM to remove it from circulation.
        </p>


        <Spacer />

        <form>

            <figure class="text-xs mb-1 opacity-50">How much?</figure>
            <div class="flex input-group input-group-divider grid-cols-[auto_1fr_auto]">
                <input type="number"
                       class="input"
                       placeholder={"bytes"}
                       bind:value={value}
                />

                <button class="btn variant-filled-primary" on:click={() => value = $accountBytes || 0}>
                    All
                </button>
            </div>

            <p class="text-xs text-right mt-1 opacity-50">You have {$accountBytes || 0} bytes</p>

            <Spacer size="20" />

            <figure class="text-xs mb-1 opacity-50">Want to enter a memo? (optional)</figure>
            <input class="input" type="text"
                   placeholder="Memo"
                   bind:value={memo}
            />


            <Spacer size="50" />

            <button class="btn variant-filled-primary w-full h-16" on:click={sellRam}>
                <i class="fa fas fa-fire"></i>
                <span class="ml-2 font-black">Burn</span>
            </button>

        </form>

    </section>

</section>

<script lang="ts">
    import Spacer from "./Spacer.svelte";
    import ChainService, {account, accountBytes} from "../services/chain.service";
    import {getToastStore, focusTrap} from "@skeletonlabs/skeleton";
    const toastStore = getToastStore();

    let value: number = 0;
    let memo: string = "";

    const sellRam = async () => {
        if (value <= 0) {
            toastStore.trigger({
                message: "Please enter a valid amount of bytes",
            });
            return;
        }

        const burned = await ChainService.burnRam(value, memo, toastStore);
        if (burned) {
            toastStore.trigger({
                message: `Successfully burned ${value} bytes`,
            });
        }
    }

</script>