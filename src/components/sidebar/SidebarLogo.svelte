<script>
    let { isOpen } = $props();
</script>

<div class="p-8 shrink-0 overflow-hidden whitespace-nowrap">
    <h2 class="text-sm font-black tracking-[0.3em] text-white uppercase italic transition-all duration-500">
        {#if isOpen}
            <span class="inline-block animate-in fade-in slide-in-from-left-4 duration-500">
                Grooming <span class="text-indigo-500 not-italic">Cut</span>
            </span>
        {:else}
            <span class="inline-block animate-in fade-in duration-500">
                G<span class="text-indigo-500 not-italic ml-1">C</span>
            </span>
        {/if}
    </h2>
    <div class="h-[1px] transition-all duration-500 bg-slate-800 mt-2 {isOpen ? 'w-6' : 'w-4'}"></div>
</div>