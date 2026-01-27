<script>
import { fade, fly } from 'svelte/transition';
import { cubicOut } from 'svelte/easing';

let { isOpen = $bindable(false), header, children, footer } = $props(); 

function close() { isOpen = false; }

function handleKeyDown(e) {
    if (e.key === 'Escape' && isOpen) {
        close();
    }
}
</script>

<svelte:window onkeydown={handleKeyDown}/>

{#if isOpen}
    <div class='fixed inset-0 z-[100] flex items-center justify-center p-4'
        transition:fade={{ duration: 300 }}
        onclick={close}
    >
        <div class='absolute inset-0 bg-black/75 backdrop-blur-3xl transition-all duration-500'></div>

        <div class='relative z-10 w-full max-w-lg bg-[#0f1115]/95 backdrop-blur-md border border-white/10 rounded-[2.5rem]
                    shadow-[0_0_100px_rgba(0,0,0,0.9)] max-h-[90vh] flex flex-col overflow-hidden'
            transition:fly={{ y: 40, duration: 500, easing: cubicOut, opacity: 0 }}
            onclick={(e) => e.stopPropagation()}
        >
            <div class='h-1.5 w-12 bg-white/10 rounded-full mx-auto mt-4 mb-2 opacity-50'></div>

            {#if header}
                <div class='px-10 pt-4 pb-4'>
                    {@render header()}
                </div>
            {/if}

            <div class='px-10 py-6 overflow-y-auto custom-scrollbar flex-1'>
                {@render children()}
            </div>

            {#if footer}
                <div class='px-10 py-8 bg-white/[0.03] border-t border-white/5'>
                    {@render footer()}
                </div>
            {/if}
        </div>
    </div>
{/if}

<style>
    .custom-scrollbar::-webkit-scrollbar {
        width: 5px;
    }
    .custom-scrollbar::-webkit-scrollbar-thumb {
        background: rgba(255, 255, 255, 0.05);
        border-radius: 20px;
    }
    .custom-scrollbar::-webkit-scrollbar-track {
        background: transparent;
    }
</style>