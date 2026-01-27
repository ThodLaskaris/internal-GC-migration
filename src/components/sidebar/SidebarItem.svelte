<script>
    let { item, active, isOpen, onclick } = $props();
</script>

<button 
    {onclick}
    class="w-full flex items-center px-4 py-3 rounded-xl transition-all duration-300 relative group
    {active ? 'bg-indigo-500/10 text-indigo-400 border border-indigo-500/20 shadow-lg' : 'text-slate-500 hover:text-slate-300 border border-transparent'}">
    
    <svg class="w-5 h-5 shrink-0 transition-transform duration-300 {active ? 'scale-110' : ''}" fill="none" stroke="currentColor" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d={item.icon}></path>
    </svg>

    <span class="ml-4 text-[10px] uppercase tracking-[0.2em] whitespace-nowrap transition-all duration-500
        {isOpen ? 'opacity-100 translate-x-0 delay-150' : 'opacity-0 -translate-x-8 pointer-events-none w-0'}">
        {item.name}
    </span>
</button>