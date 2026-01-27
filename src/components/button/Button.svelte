<script>
    let { 
        type = 'button', 
        disabled = false, 
        loading = false, 
        children, 
        onclick = () => {} 
    } = $props();
</script>

<button 
    {type}
    disabled={disabled || loading}
    onclick={onclick}
    class="relative group w-full py-4 overflow-hidden rounded-xl transition-all duration-200 active:scale-[0.98] disabled:opacity-50
    bg-[#1a1b2e] 
    border border-indigo-500/30 
    hover:border-indigo-400 
    shadow-[0_0_20px_rgba(79,70,229,0.1),inset_0_1px_1px_rgba(255,255,255,0.05)]
    text-indigo-100 font-bold uppercase tracking-[0.4em] text-[10px]"
>
    <div class='relative flex items-center justify-center gap-2 group-hover:text-white transition-colors duration-300'>
        {#if loading}
            <div class='w-3 h-3 border-2 border-white/20 border-t-white rounded-full animate-spin'></div>
        {:else}
            {@render children?.()}
            <svg xmlns="http://www.w3.org/2000/svg" class="w-3 h-3 opacity-0 -translate-x-2 group-hover:opacity-100 group-hover:translate-x-0 transition-all duration-300" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M14 5l7 7m0 0l-7 7m7-7H3" />
            </svg>
        {/if}
    </div>
</button>