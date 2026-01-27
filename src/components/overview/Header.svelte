<script>
    // Κρατάμε μόνο το activeTab για τον τίτλο
    let { activeTab } = $props();
</script>

<header class="h-20 border-b border-white/5 flex items-center justify-between px-4 bg-[#05070a]/60 backdrop-blur-md sticky top-0 z-40">
    <div class="flex items-center gap-10">
        <div>
            <span class="text-[8px] tracking-[0.4em] text-slate-600 uppercase font-black italic">Command Center</span>
            <h1 class="text-[11px] tracking-[0.2em] text-white uppercase font-bold mt-1 tracking-widest">
                Section / <span class="text-indigo-500">{activeTab}</span>
            </h1>
        </div>
    </div>

    <div class="flex items-center gap-4">
        <div class="text-right hidden sm:block">
            <p class="text-[10px] text-white font-bold uppercase tracking-tighter italic">ThodLaskaris</p>
            <p class="text-[8px] text-indigo-500 uppercase tracking-widest">Admin</p>
        </div>
        <div class="w-10 h-10 rounded-xl bg-gradient-to-br from-indigo-600 to-indigo-900 border border-white/10 shadow-lg flex items-center justify-center text-[10px] font-black text-white/50">
            TL
        </div>
    </div>
</header>