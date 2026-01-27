<script>
    import Modal from '../modal/Modal.svelte';
    import Input from '../modal/Input.svelte';
    import Select from '../modal/Select.svelte';
    import Button from '../button/Button.svelte';

    let { schedule = $bindable([]) } = $props();

    let isModalOpen = $state(false);
    
    let newAppointment = $state({
        pet: '',
        service: '',
        owner: '',
        time: '',
        notes: '' 
    });

    const services = ["Full Grooming", "Bath & Brush", "Nail Trim", "Puppy First Visit", "Sanitary Trim"];

    const today = new Date().toLocaleDateString('en-US', {
        month: 'short', day: 'numeric', year: 'numeric'
    }).toUpperCase();

    function saveAppointment() {
        if(newAppointment.pet && newAppointment.time) {
            const updatedSchedule = [...schedule, {
                ...newAppointment,
                status: 'Pending'
            }];

            // Sorting: Πρώτα status, μετά ώρα
            schedule = updatedSchedule.sort((a, b) => {
                if (a.status === 'Finished' && b.status !== 'Finished') return 1;
                if (a.status !== 'Finished' && b.status === 'Finished') return -1;
                return a.time.localeCompare(b.time);
            });

            newAppointment = { pet: '', service: '', owner: '', time: '', notes: '' };
            isModalOpen = false;
        }
    }
</script>

<div class='bg-white/[0.01] border border-white/5 rounded-[1.1rem] overflow-hidden flex flex-col h-full shadow-2xl'>
    <div class='p-3 border-b border-white/5 flex items-center justify-between bg-white/[0.01] backdrop-blur-sm'>
        <div>
            <h3 class='text-[10px] uppercase tracking-[0.5em] font-black text-indigo-500/80'>Today's Timeline</h3>
            <span class='text-[9px] text-slate-600 uppercase tracking-[0.3em] font-bold italic'>{today}</span>
        </div>

        <button 
            onclick={() => isModalOpen = true}
            class="group flex items-center gap-2 transition-all active:scale-95"
        >
            <span class="text-[9px] uppercase tracking-[0.2em] font-black text-slate-500 group-hover:text-indigo-400 transition-colors">Add Session</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="w-4 h-4 text-slate-500 group-hover:text-indigo-400 transition-colors" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="3" d="M12 4v16m8-8H4" />
            </svg>
        </button>
    </div>

    <div class='flex-1 overflow-y-auto custom-scrollbar p-6'>
        <div class="space-y-0">
            {#each schedule as item}
                <div class="group relative flex items-center gap-6 p-5 rounded-[1.1rem] transition-all duration-500 
                    {item.status === 'Ongoing' ? 'bg-indigo-500/[0.03] border border-indigo-500/20 shadow-[0_0_40px_rgba(99,102,241,0.05)]' : 'border border-transparent hover:bg-white/[0.02] hover:border-white/5'} 
                    {item.status === 'Finished' ? 'opacity-40 grayscale-[0.3]' : ''}">
                    
                    <div class="flex flex-col items-center min-w-[65px]">
                        <span class="text-[11px] font-mono font-bold tracking-tighter {item.status === 'Ongoing' ? 'text-indigo-400' : 'text-slate-500'}">
                            {item.time}
                        </span>
                        <div class="w-[1px] h-6 bg-gradient-to-b from-white/10 to-transparent mt-2 transition-all group-hover:h-8"></div>
                    </div>

                    <div class="flex-1">
                        <div class="flex items-center gap-3">
                            <h4 class="text-sm font-bold tracking-tight text-white group-hover:text-indigo-300 transition-colors">{item.pet}</h4>
                            {#if item.status === 'Ongoing'}
                                <span class="relative flex h-2 w-2">
                                    <span class="animate-ping absolute inline-flex h-full w-full rounded-[1.1rem] bg-indigo-400 opacity-75"></span>
                                    <span class="relative inline-flex rounded-full h-2 w-2 bg-indigo-500"></span>
                                </span>
                            {/if}
                        </div>
                        <p class="text-[10px] text-slate-500 uppercase tracking-widest mt-1 font-medium">
                            {item.owner} <span class="mx-2 text-white/10">•</span> {item.service}
                        </p>
                        {#if item.notes}
                            <p class="text-[9px] text-indigo-400/60 italic mt-1 font-medium tracking-wide">
                                <span class="text-indigo-500">Note:</span> {item.notes}
                            </p>
                        {/if}
                    </div>

                    <div class="text-right">
                        <span class="text-[8px] font-black uppercase tracking-[0.2em] px-3 py-1.5 rounded-xl border transition-all duration-300
                            {item.status === 'Finished' ? 'border-white/5 text-slate-700 bg-white/5' : ''} 
                            {item.status === 'Ongoing' ? 'border-indigo-500/40 text-indigo-400 bg-indigo-500/10' : ''} 
                            {item.status === 'Pending' ? 'border-white/10 text-slate-500 bg-white/[0.02]' : ''}">
                            {item.status}
                        </span>
                    </div>
                </div>
            {/each}
        </div>
    </div>
</div>

<Modal bind:isOpen={isModalOpen}>
    {#snippet header()}
        <div class="space-y-1">
            <h2 class="text-2xl font-light text-white italic">New <span class="font-bold text-indigo-400 not-italic">Appointment</span></h2>
            <p class="text-[10px] text-slate-500 uppercase tracking-widest font-bold">Add to Timeline</p>
        </div>
    {/snippet}

    <div class="space-y-6">
        <div class="grid grid-cols-2 gap-4">
            <Input label="Pet Name" placeholder="e.g. Buddy" bind:value={newAppointment.pet} />
            <Input label="Time" type="time" bind:value={newAppointment.time} />
        </div>
        <Input label="Owner" placeholder="e.g. Nick" bind:value={newAppointment.owner} />
        <Select label="Service" options={services} bind:value={newAppointment.service} />
        
        <Input label="Quick Notes" placeholder="e.g. Sensitive skin, aggressive..." bind:value={newAppointment.notes} />
    </div>

    {#snippet footer()}
        <div class="flex items-center gap-6">
            <button onclick={() => isModalOpen = false} class="py-4 text-slate-500 font-black text-[10px] uppercase tracking-widest hover:text-white transition-colors">Cancel</button>
            <div class="flex-1">
                <Button onclick={saveAppointment}>Confirm Appointment</Button>
            </div>
        </div>
    {/snippet}
</Modal>

<style>
    .custom-scrollbar::-webkit-scrollbar { width: 4px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.05); border-radius: 10px; }
</style>