<section class="flex min-h-full w-full items-center justify-center">
    <section class="min-w-full md:min-w-[400px] card variant-glass md:p-8 p-4">

        <h1 class="h1">Buy RAM</h1>
        <p class="text-xs mt-3 mb-10">
            Buy RAM for your account or for someone else.
        </p>


        <Spacer />

        <form>

            <div class="space-y-2">
                <label class="flex items-center space-x-2">
                    <input class="radio" type="radio" checked name="radio-direct" value="1" on:change={() => toSelf = true} />
                    <p>Buy for me <span class="italic">({$account})</span></p>
                </label>
                <label class="flex items-center space-x-2">
                    <input class="radio" type="radio" name="radio-direct" value="2" on:change={() => toSelf = false  } />
                    <p>Buy for someone else</p>
                </label>
            </div>

            <Spacer size="20" />

            {#if !toSelf}
                <figure class="text-xs mb-1 opacity-50">Recipient</figure>
                <input class="input" type="text"
                       placeholder="Account name"
                       bind:value={receiver}
                />
                <Spacer />
            {/if}

            <figure class="text-xs mb-1 opacity-50">How much?</figure>
            <div class="input-group input-group-divider grid-cols-[auto_1fr_auto]">
                <input type="number"
                       class="input"
                       placeholder={placeholder}
                       bind:value={value}
                />

                <select bind:value={type} class="select" on:change={changedType}>
                    <option>EOS</option>
                    <option>Bytes</option>
                </select>
            </div>

            <Spacer size="50" />

            <button class="btn variant-filled-primary w-full h-16" on:click={buyRam}>
                <i class="fa fas fa-up"></i>
                <span class="ml-2 font-black">Buy</span>
            </button>

        </form>

    </section>

</section>

<script lang="ts">
    import Spacer from "./Spacer.svelte";
    import ChainService, {account} from "../services/chain.service";
    import {getToastStore} from "@skeletonlabs/skeleton";
    const toastStore = getToastStore();

    let receiver: string = "";
    let toSelf: boolean = true;
    let type: string = "EOS";
    let value: number = 0;

    $: isBytes = type === "Bytes";

    const changedType = () => {
        console.log(type);
    }

    $: placeholder = type === "EOS" ? "1.0000" : "bytes";

    const buyRam = async () => {
        if (value <= 0) {
            toastStore.trigger({
                message: isBytes ? "Please enter a valid amount of bytes" : "Please enter a valid amount of EOS",
            });
            return;
        }
        const _receiver:string = toSelf ? $account as string : receiver;

        if (!_receiver || !_receiver.length) {
            toastStore.trigger({
                message: "Please enter a valid account name",
            });
            return;
        }

        const bought = await ChainService.buyRam(_receiver, value, isBytes, toastStore);
        if (bought) {
            toastStore.trigger({
                message: `Successfully bought ${value} ${type} for ${_receiver}`,
            });
        }
    }

</script>