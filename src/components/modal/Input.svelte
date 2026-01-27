<script>
    /**
     * Svelte 5 Props (Raw JS)
     * label: Ο τίτλος πάνω από το input
     * value: Το περιεχόμενο (bindable για να το διαβάζει ο parent)
     * type: text, password, email, number, κλπ.
     * placeholder: Το κείμενο "φάντασμα" μέσα στο input
     */
    let { 
        label, 
        value = $bindable(''), 
        type = 'text', 
        placeholder = '' 
    } = $props();
</script>

<div class='flex flex-col gap-1 w-full'>
    {#if label}
        <label class='text-[10px] uppercase tracking-[0.25em] text-slate-500 font-black ml-1'>
            {label}
        </label>
    {/if}
    
    <input 
        {type}
        {placeholder}
        bind:value={value}
        class='w-full bg-white/[0.03] border border-white/10 rounded-[0.9rem] px-5 py-4
               text-white placeholder:text-slate-700 outline-none transition-all duration-300
               focus:border-indigo-500/40 focus:bg-white/[0.05] focus:ring-4 focus:ring-indigo-500/10'
    />
</div>