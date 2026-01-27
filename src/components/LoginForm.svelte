<script>
    import Button from './button/Button.svelte';
    let username = $state('');
    let password = $state('');
    let loading = $state(false);

    function handleLogin(e) {
        e.preventDefault();
        loading = true;
        setTimeout(() => {
            loading = false;
            window.location.href = '/overview'; 
        }, 1500);
    }
</script>

<form 
    onsubmit={handleLogin}
    class='relative w-full max-w-sm bg-[#0a0f1a]/80 border border-white/5 p-12 rounded-[1.1rem] backdrop-blur-3xl shadow-[0_20px_50px_rgba(0,0,0,0.5)] transition-all duration-500 hover:border-indigo-500/30 group/form'
>
    <div class="absolute top-0 left-1/2 -translate-x-1/2 w-1/3 h-[1px] bg-gradient-to-r from-transparent via-indigo-500 to-transparent"></div>

    <header class='flex flex-col items-center mb-12 text-center'>
        <div class='relative mb-6'>
            <div class="absolute inset-0 bg-indigo-500 blur-2xl opacity-20 group-hover/form:opacity-40 transition-opacity"></div>
            <div class='relative w-14 h-14 bg-black border border-white/10 rounded-[1.1rem] flex items-center justify-center text-xl shadow-2xl'>
                ✂️
            </div>
        </div>
        
        <h1 class='text-xl font-light tracking-[0.3em] text-white uppercase'>
            Grooming <span class='font-black text-indigo-500'>Cut</span>
        </h1>
        <div class="h-[1px] w-8 bg-slate-700 my-3"></div>
        <p class='text-[9px] font-medium tracking-[0.4em] text-slate-500 uppercase italic'>
            Enterprise Access Control
        </p>
    </header>

    <section class='flex flex-col gap-5'>
        <div class="relative">
            <input 
                type='text'
                bind:value={username}
                placeholder='Username'
                class='w-full bg-black/40 border border-white/[0.03] p-4 pl-5 rounded-[1.1rem] text-white text-[11px] tracking-[0.1em] focus:border-indigo-500/50 focus:bg-black/60 outline-none transition-all placeholder:text-slate-700 font-mono'
                required
            />
        </div>
        
        <div class="relative">
            <input 
                type='password'
                bind:value={password}
                placeholder='Password'
                class='w-full bg-black/40 border border-white/[0.03] p-4 pl-5 rounded-xl text-white text-[11px] tracking-[0.1em] focus:border-indigo-500/50 focus:bg-black/60 outline-none transition-all placeholder:text-slate-700 font-mono'
                required
            />
        </div>
    </section>
    
    <footer class='mt-6 text-center'>
        <Button type='submit' 
        {loading}
        >
            ACCESS
        </Button>
        
        <div class="mt-4">
            <!-- svelte-ignore a11y_invalid_attribute -->
            <a href="#" class="text-[8px] text-slate-600 hover:text-indigo-400 transition-colors tracking-widest uppercase">
                Reset Credentials
            </a>
        </div>
    </footer>
</form>