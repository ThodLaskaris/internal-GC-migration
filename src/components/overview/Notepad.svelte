<script>
    let { notes = $bindable() } = $props();
    let newNote = $state("");

    function addNote(e) {
        if (e.key === 'Enter' && newNote.trim() !== "") {
            notes.push({ id: Date.now(), text: newNote, done: false });
            newNote = "";
        }
    }
</script>

<div class='bg-white/[0.02] border border-white/5 rounded-[1.1rem] p-8 flex flex-col h-full min-h-[300px]'>
    <h3 class='text-[9px] uppercase tracking-[0.4em] font-black text-slate-500 mb-6'>Notes</h3>

    <div class='space-y-4 flex-1 overflow-y-auto pr-2 custom-scrollbar'>
        {#each notes as note}
        <button 
            onclick={() => note.done = !note.done}
            class='flex items-start gap-3 group w-full text-left transition-opacity {note.done ? 'opacity-40' : 'opacity-100'}'>
            <div class='w-4 h-4 mt-0.5 rounded border border-white/10 flex items-center justify-center transition-all {note.done ? 'bg-indigo-500 border-indigo-500' : 'group-hover:border-indigo-500'}'>
                {#if note.done} <span class='text-[8px] text-white'>✓</span> {/if}
            </div>
            <span class='text-[11px] tracking-wide {note.done ? 'line-through text-slate-600' : 'text-slate-300'}'>{note.text}</span>
        </button>
        {/each}
    </div>

    <div class="mt-6 pt-6 border-t border-white/5">
        <input 
            type="text" 
            bind:value={newNote}
            onkeydown={addNote}
            placeholder="Add a quick note..."
            class="w-full bg-white/[0.03] border border-white/10 rounded-xl px-4 py-3 text-[10px] text-slate-300 placeholder:text-slate-600 focus:outline-none focus:border-indigo-500/50 transition-all"
        />
    </div>
</div>

<style>
    .custom-scrollbar::-webkit-scrollbar { width: 4px; }
    .custom-scrollbar::-webkit-scrollbar-thumb { background: rgba(255,255,255,0.05); border-radius: 10px; }
</style>