<script>
    let { isOpen } = $props();
    let version = "1.0.4-stable"; // Πλέον ζει εδώ
</script>

<div class="p-4 border-t border-white/5 bg-black/20 overflow-hidden shrink-0">
    <div class="flex items-center gap-3 opacity-40 hover:opacity-100 transition-all duration-300 group/source cursor-default">
         <svg xmlns="http://www.w3.org/2000/svg" width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" class="text-indigo-500 shrink-0">
            <circle cx="12" cy="18" r="3"></circle><circle cx="6" cy="6" r="3"></circle><circle cx="18" cy="6" r="3"></circle>
            <path d="M18 9v2c0 .6-.4 1-1 1H7c-.6 0-1-.4-1-1V9"></path><path d="M12 12v3"></path>
        </svg>
        <div class="flex flex-col transition-all duration-500 {isOpen ? 'opacity-100 translate-x-0 delay-150' : 'opacity-0 -translate-x-8 w-0'}">
            <span class="text-[8px] font-black uppercase tracking-[0.2em] text-slate-500 whitespace-nowrap">Source Control</span>
            <span class="text-[10px] font-mono text-indigo-400/80 mt-0.5 uppercase tracking-tighter">v.{version}</span>
        </div>
    </div>
</div>