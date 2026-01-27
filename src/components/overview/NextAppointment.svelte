<script>
    let { appointment } = $props();
</script>

<div class='relative group overflow-hidden bg-white/[0.01] backdrop-blur-xl border border-white/10 rounded-[1.1rem] p-8 transition-all duration-500 hover:border-indigo-500/30 hover:bg-white/[0.03] shadow-[0_20px_50px_rgba(0,0,0,0.5)]'>
    
    <div class='absolute -right-12 -top-12 w-32 h-32 bg-indigo-500/10 blur-[50px] rounded-full group-hover:bg-indigo-500/20 transition-all'></div>
    <div class='absolute inset-px  bg-gradient-to-br from-white/[0.05] to-transparent pointer-events-none'></div>

    <div class='relative z-10 space-y-8'>
        <div class='flex justify-between items-center'>
            <div class='flex items-center gap-2'>
                <div class='w-1 h-1 rounded-full bg-indigo-500 shadow-[0_0_10px_#6366f1]'></div>
                <span class='text-[8px] font-black uppercase tracking-[0.3em] text-slate-500'>Live Session</span>
            </div>
            <span class='text-3xl font-mono text-white tracking-tighter tabular-nums opacity-90'>{appointment.time}</span>
        </div>

        <div class='space-y-1'>
            <h2 class='text-4xl font-light text-white tracking-tight'>
                {appointment.petName}
            </h2>
            <p class='text-sm text-slate-400 font-medium tracking-wide'>
                {appointment.owner} <span class='mx-2 text-white/5'>|</span> <span class='text-[10px] text-slate-500 uppercase tracking-widest font-bold'>{appointment.breed}</span>
            </p>
        </div>

        <div class='grid grid-cols-2 gap-4 pt-6 border-t border-white/5'>
            <div class='space-y-1'>
                <p class='text-[7px] uppercase tracking-widest text-slate-600 font-black'>Service</p>
                <p class='text-[11px] text-indigo-400/90 font-bold tracking-wide uppercase'>{appointment.service}</p>
            </div>
            <div class='space-y-1 text-right'>
                <p class='text-[7px] uppercase tracking-widest text-slate-600 font-black'>Contact</p>
                <p class='text-[11px] text-slate-400 font-mono'>{appointment.phone}</p>
            </div>
        </div>

        <div class='bg-black/20 rounded-[1.1rem] p-4 border border-white/5 group-hover:bg-black/40 transition-colors'>
            <p class='text-[7px] uppercase tracking-widest text-indigo-500 font-black mb-2'>Instructions</p>
            <p class='text-[12px] text-slate-400 leading-relaxed italic font-medium'>
                "{appointment.notes}"
            </p>
        </div>
    </div>
</div>