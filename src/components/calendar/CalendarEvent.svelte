<script>
    // Στη Svelte 5 χρησιμοποιούμε $props()
    let { calendarEvent } = $props();
</script>

<div class="h-full w-full p-2 rounded-lg border-l-4 backdrop-blur-md flex flex-col overflow-hidden transition-all hover:brightness-110"
     style="border-color: {calendarEvent.color === 'indigo' ? '#6366f1' : '#10b981'}; 
            background: {calendarEvent.color === 'indigo' ? 'rgba(99, 102, 241, 0.15)' : 'rgba(16, 185, 129, 0.15)'};">
    <span class="text-[8px] font-black text-white/50 uppercase">
        {calendarEvent.start.split('T')[1].substring(0,5)}
    </span>
    <span class="text-xs font-bold text-white truncate">{calendarEvent.title}</span>
    <span class="text-[9px] text-white/70 mt-auto font-medium uppercase">{calendarEvent.type || ''}</span>
</div>