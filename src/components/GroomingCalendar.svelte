<script>
    import Button from './button/Button.svelte';

    let views = ['Day', 'Week', 'Month'];
    let activeView = $state('Day');

    // Mock ραντεβού για το Scheduler
    let appointments = $state([
        { 
            id: 1, 
            time: "09:30 - 11:00", 
            pet: "Luna", 
            owner: "George P.", 
            service: "Full Grooming", 
            type: "full", // indigo
            top: 40, // Υπολογισμένο top (9:30)
            height: 120 // Διάρκεια 1.5 ώρα
        },
        { 
            id: 2, 
            time: "12:00 - 12:45", 
            pet: "Max", 
            owner: "Sarah L.", 
            service: "Bath & Brush", 
            type: "bath", // emerald
            top: 240, 
            height: 60 
        },
        { 
            id: 3, 
            time: "14:00 - 15:30", 
            pet: "Bella", 
            owner: "Nick K.", 
            service: "Scissor Cut", 
            type: "trim", // purple
            top: 400, 
            height: 120 
        }
    ]);

    const hours = Array.from({ length: 11 }, (_, i) => i + 9); // 09:00 - 19:00
</script>

<div class="space-y-8 animate-in fade-in slide-in-from-bottom-4 duration-700">
    
    <div class="flex flex-col md:flex-row justify-between items-start md:items-center gap-4">
        <div class="flex items-center gap-6">
            <div class="flex flex-col">
                <span class="text-[9px] uppercase tracking-[0.4em] text-slate-500 font-black italic">Scheduler</span>
                <h2 class="text-2xl font-light text-white tracking-tighter">Monday, Jan 26</h2>
            </div>
            
            <div class="flex gap-1 bg-white/[0.03] p-1 rounded-xl border border-white/5 backdrop-blur-md">
                {#each views as view}
                    <button 
                        onclick={() => activeView = view}
                        class="px-5 py-1.5 rounded-lg text-[9px] uppercase font-black tracking-widest transition-all
                        {activeView === view ? 'bg-indigo-500 text-white shadow-lg' : 'text-slate-500 hover:text-slate-300'}">
                        {view}
                    </button>
                {/each}
            </div>
        </div>

        <div class="flex items-center gap-3">
            <div class="flex bg-white/[0.03] rounded-xl border border-white/5 overflow-hidden">
                <button class="p-2.5 hover:bg-white/5 text-slate-400 border-r border-white/5">←</button>
                <button class="px-4 py-2 text-[10px] uppercase font-black tracking-widest text-slate-300 hover:bg-white/5">Today</button>
                <button class="p-2.5 hover:bg-white/5 text-slate-400 border-l border-white/5">→</button>
            </div>
            <Button>+ New Appointment</Button>
        </div>
    </div>

    <div class="bg-[#0a0f1a]/40 border border-white/5 rounded-[2.5rem] overflow-hidden backdrop-blur-xl relative shadow-2xl">
        
        <div class="grid grid-cols-[100px_1fr] border-b border-white/5 bg-white/[0.02]">
            <div class="p-4 border-r border-white/5 flex items-center justify-center">
                <span class="text-[9px] text-slate-600 font-black uppercase">Time</span>
            </div>
            <div class="p-4 px-10">
                <span class="text-[10px] text-indigo-400 font-black uppercase tracking-[0.2em]">Active Timeline</span>
            </div>
        </div>

        <div class="grid grid-cols-[100px_1fr] relative h-[880px] overflow-y-auto custom-scrollbar">
            
            <div class="bg-black/20 border-r border-white/5 relative z-10">
                {#each hours as hour}
                    <div class="h-20 border-b border-white/10 flex items-start justify-center pt-2">
                        <span class="text-[10px] font-mono text-slate-600 tracking-tighter font-bold uppercase">{hour}:00</span>
                    </div>
                {/each}
            </div>

            <div class="relative bg-[linear-gradient(rgba(255,255,255,0.03)_1px,transparent_1px)] bg-[size:100%_80px]">
                
                <div class="absolute top-[380px] left-0 right-0 z-20 flex items-center pointer-events-none">
                    <div class="w-2 h-2 rounded-full bg-red-500 shadow-[0_0_10px_red]"></div>
                    <div class="flex-1 h-[1px] bg-red-500/40 border-dashed border-t"></div>
                </div>

                {#each appointments as appt}
                    <div 
                        class="absolute left-6 right-10 rounded-[1.5rem] p-5 border-l-4 transition-all duration-300 cursor-pointer group hover:scale-[1.01] hover:shadow-2xl z-10
                        {appt.type === 'full' ? 'bg-indigo-500/10 border-indigo-500 hover:bg-indigo-500/20' : ''}
                        {appt.type === 'bath' ? 'bg-emerald-500/10 border-emerald-500 hover:bg-emerald-500/20' : ''}
                        {appt.type === 'trim' ? 'bg-purple-500/10 border-purple-500 hover:bg-purple-500/20' : ''}"
                        style="top: {appt.top}px; height: {appt.height}px;"
                    >
                        <div class="flex justify-between items-start">
                            <div>
                                <span class="text-[9px] font-black uppercase tracking-widest opacity-60 {appt.type === 'full' ? 'text-indigo-400' : ''} {appt.type === 'bath' ? 'text-emerald-400' : ''} {appt.type === 'trim' ? 'text-purple-400' : ''}">
                                    {appt.time}
                                </span>
                                <h4 class="text-white text-base font-bold tracking-tight mt-1">{appt.pet}</h4>
                                <p class="text-[10px] text-slate-400 uppercase tracking-tighter mt-1">{appt.owner} • {appt.service}</p>
                            </div>
                            
                            <button class="opacity-0 group-hover:opacity-100 p-2 bg-white/5 rounded-lg transition-opacity">
                                <span class="text-xs">→</span>
                            </button>
                        </div>
                    </div>
                {/each}
            </div>
        </div>
    </div>
</div>

<style>
    .custom-scrollbar::-webkit-scrollbar {
        width: 4px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
        background: rgba(255, 255, 255, 0.05);
        border-radius: 10px;
    }
</style>