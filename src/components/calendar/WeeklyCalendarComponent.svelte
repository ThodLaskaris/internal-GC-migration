<script>
    import { onMount, onDestroy } from 'svelte';
    import { Calendar } from '@fullcalendar/core';
    import timeGridPlugin from '@fullcalendar/timegrid';
    import interactionPlugin from '@fullcalendar/interaction';

    let calendarEl;
    let calendar;
    let resizeObserver;
    let currentTitle = $state("");
    let activeView = $state("timeGridWeek");

    onMount(() => {
        calendar = new Calendar(calendarEl, {
            plugins: [timeGridPlugin, interactionPlugin],
            initialView: activeView,
            locale: 'en',
            firstDay: 1,
            slotMinTime: '10:00:00',
            slotMaxTime: '22:00:00',
            allDaySlot: false,
            headerToolbar: false,
            height: '100%',
            
            slotDuration: '00:30:00',
            snapDuration: '00:05:00',
            slotLabelInterval: '01:00:00',
            nowIndicator: true,
            
            editable: true, 
            droppable: true,
            dragRevertDuration: 0, 
            eventDragMinDistance: 1,
            eventMirror: true, 
            dragScroll: true, // Επιτρέπει ομαλό scrolling κατά το drag

            eventDrop: (info) => {
                console.log(`Event moved to: ${info.event.start.toISOString()}`);
            },
            eventResize: (info) => {
                console.log(`Event duration changed`);
            },

            businessHours: [
                { daysOfWeek: [ 2, 3, 4, 5 ], startTime: '10:00', endTime: '22:00' },
                { daysOfWeek: [ 6 ], startTime: '10:00', endTime: '17:00' }
            ],
            selectConstraint: 'businessHours',
            eventConstraint: 'businessHours',
            datesSet: (info) => {
                currentTitle = info.view.title;
                activeView = info.view.type;
            },
            events: [
                { 
                    title: 'Luna - Grooming', 
                    start: '2026-01-27T10:30:00', 
                    end: '2026-01-27T12:00:00', 
                    backgroundColor: 'rgba(99, 102, 241, 0.12)',
                    borderColor: '#6366f1',
                    extendedProps: { type: 'Full Grooming', color: 'indigo' } 
                },
                { 
                    title: 'Max - Bath', 
                    start: '2026-01-28T14:00:00', 
                    end: '2026-01-28T15:30:00', 
                    backgroundColor: 'rgba(16, 185, 129, 0.12)',
                    borderColor: '#10b981',
                    extendedProps: { type: 'Bath & Brush', color: 'emerald' } 
                }
            ],
            eventContent: (arg) => {
                const isIndigo = arg.event.extendedProps.color === 'indigo';
                const color = isIndigo ? '#6366f1' : '#10b981';
                const bgColor = isIndigo ? 'rgba(99, 102, 241, 0.15)' : 'rgba(16, 185, 129, 0.15)';
                let container = document.createElement('div');
                container.className = 'h-full w-full p-2 rounded-lg backdrop-blur-md border border-white/5 flex flex-col overflow-hidden cursor-grab active:cursor-grabbing';
                container.style.backgroundColor = bgColor;
                container.style.borderLeft = `3px solid ${color}`;
                container.innerHTML = `
                    <span class="text-[8px] font-black text-white/40 uppercase tabular-nums">${arg.timeText}</span>
                    <span class="text-xs font-bold text-white truncate mt-0.5">${arg.event.title}</span>
                    <span class="text-[9px] text-white/60 font-medium mt-auto uppercase tracking-tighter">${arg.event.extendedProps.type || ''}</span>
                `;
                return { domNodes: [container] };
            }
        });

        calendar.render();
        resizeObserver = new ResizeObserver(() => calendar?.updateSize());
        resizeObserver.observe(calendarEl);
    });

    const setView = (v) => calendar.changeView(v);
    const next = () => calendar.next();
    const prev = () => calendar.prev();
    const today = () => calendar.today();

    onDestroy(() => { 
        if (resizeObserver) resizeObserver.disconnect();
        if (calendar) calendar.destroy(); 
    });
</script>

<div class="flex flex-col h-full overflow-hidden bg-[#0a0c10] font-sans">
    <div class="flex items-center justify-between px-8 py-5 border-b border-white/5 bg-black/40 backdrop-blur-xl shrink-0 z-30">
        <div class="flex items-center gap-5">
            <div>
                <h2 class="text-xl font-black text-white tracking-tighter leading-none uppercase">{currentTitle}</h2>
                <p class="text-[8px] font-bold uppercase tracking-[0.4em] text-indigo-500 mt-1 italic opacity-80">Scheduler Pro</p>
            </div>
            <div class="flex items-center gap-2 ml-4">
                <button onclick={() => setView('timeGridDay')} class="px-4 py-2 rounded-lg transition-all duration-200 active:scale-95 text-[9px] font-bold uppercase tracking-widest border {activeView === 'timeGridDay' ? 'bg-indigo-600/20 border-indigo-500 text-white shadow-[0_0_15px_rgba(99,102,241,0.3)]' : 'bg-white/5 border-white/5 text-slate-400 hover:border-white/20 hover:text-white'}">Day</button>
                <button onclick={() => setView('timeGridWeek')} class="px-4 py-2 rounded-lg transition-all duration-200 active:scale-95 text-[9px] font-bold uppercase tracking-widest border {activeView === 'timeGridWeek' ? 'bg-indigo-600/20 border-indigo-500 text-white shadow-[0_0_15px_rgba(99,102,241,0.3)]' : 'bg-white/5 border-white/5 text-slate-400 hover:border-white/20 hover:text-white'}">Week</button>
            </div>
        </div>
        <div class="flex items-center gap-3">
            <button onclick={today} class="px-5 py-2 text-[9px] font-bold uppercase tracking-widest text-white bg-white/5 border border-white/10 rounded-lg hover:bg-white/10 hover:border-indigo-500/50 transition-all active:scale-95">Today</button>
            <div class="flex bg-white/5 rounded-lg border border-white/10 overflow-hidden backdrop-blur-md">
                <button onclick={prev} class="p-2 px-4 hover:bg-white/10 text-white border-r border-white/10 transition-colors active:bg-indigo-500/20"><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m15 18-6-6 6-6"/></svg></button>
                <button onclick={next} class="p-2 px-4 hover:bg-white/10 text-white transition-colors active:bg-indigo-500/20"><svg xmlns="http://www.w3.org/2000/svg" width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="3" stroke-linecap="round" stroke-linejoin="round"><path d="m9 18 6-6-6-6"/></svg></button>
            </div>
        </div>
    </div>
    <div class="flex-1 overflow-hidden bg-[#0a0c10]">
        <div bind:this={calendarEl} class="h-full"></div>
    </div>
</div>

<style>
    :global(:root) {
        --fc-border-color: rgba(255, 255, 255, 0.03);
        --fc-now-indicator-color: #6366f1;
        --fc-today-bg-color: rgba(99, 102, 241, 0.02);
    }
    :global(.fc-scroller::-webkit-scrollbar) { display: none; }
    :global(.fc-scroller) { -ms-overflow-style: none; scrollbar-width: none; }
    :global(.fc-theme-standard .fc-scrollgrid) { border: none !important; }
    
    :global(.fc-timegrid-slot) { height: 45px !important; }
    :global(.fc-col-header-cell) { padding: 12px 0 !important; border-bottom: 1px solid rgba(255, 255, 255, 0.05) !important; }
    :global(.fc-col-header-cell-cushion) { font-size: 9px; font-weight: 800; color: #475569; text-transform: uppercase; text-decoration: none !important; }
    :global(.fc-day-today .fc-col-header-cell-cushion) { color: white !important; background: #6366f1; padding: 2px 10px !important; border-radius: 4px; }
    :global(.fc-timegrid-slot-label-cushion) { font-size: 8px; color: #334155; font-weight: 700; }
    
    /* FIX ΓΙΑ SMOOTH ANIMATION ΜΕΤΑΞΥ ΣΤΗΛΩΝ */
    :global(.fc-event-mirror) {
        transition: transform 0.05s linear !important; /* Πολύ μικρό transition για να "γλιστράει" αντί να πηδάει */
        z-index: 9999 !important;
        pointer-events: none !important; /* Κρίσιμο: αποτρέπει το "τρεμούλιασμα" κατά την αλλαγή στήλης */
        will-change: transform, top, left;
        opacity: 1 !important;
        border: none !important;
        box-shadow: 0 20px 50px rgba(0,0,0,0.8) !important;
    }

    :global(.fc-event-dragging) {
        opacity: 0.3 !important;
    }

    :global(.fc-timegrid-event-harness-indicator) {
        display: none !important;
    }

    :global(.fc-v-event) { 
        background: transparent !important; 
        border: none !important;
    }

    :global(.fc-non-business), :global(.fc-day-sun), :global(.fc-day-mon) {
        background: rgba(255, 255, 255, 0.01) !important;
        backdrop-filter: blur(4px);
    }
</style>