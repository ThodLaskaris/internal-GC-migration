<script>
    import Sidebar from '../sidebar/Sidebar.svelte'; 
    import StatsGrid from './StatsGrid.svelte';
    import NextSession from './NextAppointment.svelte';
    import Scratchpad from './Notepad.svelte';
    import Timeline from './Timeline.svelte';
    import Header from './Header.svelte';
    import WeeklyCalendarComponent from '../calendar/WeeklyCalendarComponent.svelte';
    
    let activeTab = $state('overview');

    let stats = $state([
        { label: "Total Customers", value: "123", color: "text-indigo-400" },
        { label: "Total Pets", value: "456", color: "text-indigo-400" },
        { label: "Total Appointments", value: "789", color: "text-indigo-400" },        
        { label: "Pending Revenue", value: "€ 10.112", color: "text-emerald-400" },
    ]);

    let nextAppointment = $state({
        petName: "Luna", breed: "Golden Retriever", owner: "George P.",
        time: "14:30", phone: "698 123 4567", service: "Full Grooming",
        notes: "Sensitive skin - use organic shampoo."
    });

    let quickNotes = $state([
        { id: 1, text: "Order special shampoo for Luna", done: false },
        { id: 2, text: "Call Mrs. Maria for reschedule", done: true }
    ]);

    let schedule = $state([
        { time: "09:00", pet: "Max", owner: "Alex", service: "Bath", status: "Finished" },
        { time: "11:30", pet: "Bella", owner: "Sophie", service: "Nail Trim", status: "Finished" },
        { time: "13:00", pet: "Charlie", owner: "David", service: "Haircut", status: "Finished" },
        { time: "14:30", pet: "Luna", owner: "George", service: "Full", status: "Ongoing" },
        { time: "16:00", pet: "Bella", owner: "Sophie", service: "Nail Trim", status: "Pending" },
        { time: "17:30", pet: "Charlie", owner: "David", service: "Haircut", status: "Pending" }
    ]);

    const finishedCount = $derived(schedule.filter(i => i.status === 'Finished').length);
    const progressPercent = $derived(schedule.length > 0 ? Math.round((finishedCount / schedule.length) * 100) : 0);
</script>

<div class="flex h-screen bg-[#05070a] text-slate-200 font-sans overflow-hidden relative">
    
    <div class="fixed inset-0 pointer-events-none">
        <div class="absolute top-0 left-0 w-full h-full bg-gradient-to-br from-indigo-500/[0.03] to-transparent"></div>
    </div>

    <Sidebar bind:activeTab={activeTab} />

    <main class="relative z-10 flex-1 flex flex-col min-h-0">
        
        <Header {activeTab} />

        <section class="p-3 w-full max-w-full mx-auto flex flex-col gap-2 flex-1 overflow-hidden">
            {#if activeTab === 'overview'}
                
                <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-2 shrink-0">
                    <StatsGrid {stats} />
                </div>
                
                <div class="grid grid-cols-1 lg:grid-cols-12 gap-2 items-stretch flex-1 min-h-0">
                    
                    <div class="lg:col-span-9 flex flex-col gap-2 min-h-0"> 
                        <div class="flex-1 min-h-0 overflow-hidden">
                            <Timeline bind:schedule={schedule} />
                        </div>
                    </div>

                    <div class="lg:col-span-3 flex flex-col gap-2 min-h-0">
                        <div class="shrink-0">
                            <NextSession appointment={nextAppointment} />
                        </div>
                        <div class="flex-1 min-h-0">
                            <Scratchpad bind:notes={quickNotes} />
                        </div>
                    </div>
                </div>
                
            {:else if activeTab === 'calendar'}
                <div class="flex-1 min-h-0 overflow-hidden bg-[#0a0c10]/50 rounded-[1.1rem] border border-white/5 shadow-2xl">
                    <WeeklyCalendarComponent />
                </div>
            {:else}
                <div class="flex-1 flex items-center justify-center border border-dashed border-white/10 rounded-[1.1rem]">
                    <p class="text-slate-500 uppercase text-[10px] tracking-widest font-bold italic">
                        Module {activeTab} is coming soon...
                    </p>
                </div>
            {/if}
        </section>
    </main>
</div>

<style>
    :global(.custom-scrollbar::-webkit-scrollbar) {
        width: 4px;
    }
    :global(.custom-scrollbar::-webkit-scrollbar-track) {
        background: transparent;
    }
    :global(.custom-scrollbar::-webkit-scrollbar-thumb) {
        background: rgba(255, 255, 255, 0.05);
        border-radius: 10px;
    }
</style>