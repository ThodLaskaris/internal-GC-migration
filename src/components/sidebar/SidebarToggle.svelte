<script>
    let { isOpen = $bindable() } = $props();
</script>

<div 
    role="none"
    class="absolute -right-4 top-0 bottom-0 w-8 z-[100] cursor-pointer flex items-center justify-center group"
    onclick={() => isOpen = !isOpen}
>
    <div class="flex flex-col items-center pointer-events-none">
        <div class="w-[1px] h-12 bg-gradient-to-t from-indigo-500/40 to-transparent transition-all duration-500 group-hover:h-20 group-hover:from-indigo-400"></div>
        <div class="w-1.5 h-1.5 rounded-full bg-indigo-500 shadow-[0_0_15px_rgba(99,102,241,0.8)] border border-white/20 my-2 transition-transform duration-500 group-hover:scale-150"></div>
        <div class="w-[1px] h-12 bg-gradient-to-b from-indigo-500/40 to-transparent transition-all duration-500 group-hover:h-20 group-hover:from-indigo-400"></div>
    </div>
</div>