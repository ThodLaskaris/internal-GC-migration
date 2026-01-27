<script>
    let { 
        label, 
        value = $bindable(''), 
        options = [], 
        placeholder = 'Select service...' 
    } = $props();
</script>

<div class='flex flex-col gap-2 w-full'>
    {#if label}
        <label class='text-[10px] uppercase tracking-[0.2em] text-slate-500 font-black ml-1'>
            {label}
        </label>
    {/if}

    <div class="relative group">
        <select 
            bind:value={value}
            class='w-full bg-white/[0.03] border border-white/10 rounded-2xl px-5 py-4
                   text-white appearance-none outline-none transition-all duration-300 cursor-pointer
                   focus:border-indigo-500/40 focus:bg-white/[0.06] focus:ring-4 focus:ring-indigo-500/5'
        >
            <option value="" disabled selected>{placeholder}</option>
            {#each options as option}
                <option value={option} class="bg-[#0a0b14] text-white">
                    {option}
                </option>
            {/each}
        </select>
        
        <div class="absolute right-5 top-1/2 -translate-y-1/2 pointer-events-none text-slate-600 group-focus-within:text-indigo-400 transition-colors">
            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M19 9l-7 7-7-7" />
            </svg>
        </div>
    </div>
</div>