<script>
    import SidebarItem from './SidebarItem.svelte';
    import SidebarLogo from './SidebarLogo.svelte';
    import SidebarToggle from './SidebarToggle.svelte';
    import SidebarFooter from './SidebarFooter.svelte';
    import { menuItems } from './SidebarElements.js';

    let { activeTab = $bindable(), isOpen = $bindable(true) } = $props();
</script>

<aside class="relative border-r border-white/5 bg-[#0a0f1a]/50 backdrop-blur-xl flex flex-col h-full transition-all duration-500 ease-[cubic-bezier(0.4,0,0.2,1)]
    {isOpen ? 'w-64' : 'w-20'}">
    
    <SidebarToggle bind:isOpen />
    <SidebarLogo {isOpen} />

    <nav class="flex-1 px-4 space-y-2 mt-4 overflow-hidden">
        {#each menuItems as item}
            <SidebarItem 
                {item} 
                {isOpen} 
                active={activeTab === item.id} 
                onclick={() => activeTab = item.id} 
            />
        {/each}
    </nav>
    
    <SidebarFooter {isOpen} />
</aside>