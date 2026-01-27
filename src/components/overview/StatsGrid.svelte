<script>
    let {stats} = $props();
</script>

    {#each stats as stat}
        <div class='bg-white/[0.02] border border-white/5 rounded-[1rem] py-2 px-2 hover:bg-white/[0.04] 
        hover:border-white/10 transition-all flex justify-between items-center group'>
            <div class='flex flex-col gap-0'>
                <p class='text-[8px] uppercase tracking-[0.4em] text-slate-500 font-black group-hover:text-slate-400 transition-colors'>{stat.label}</p>
                <p class='text-xl font-light tracking-tighter {stat.color}'>{stat.value}</p>    
            </div>
            <div class='h-5 w-[1px] bg-white/5 group-hover:bg-indigo-500/30 transition-colors'></div>
        </div>
        {/each}
