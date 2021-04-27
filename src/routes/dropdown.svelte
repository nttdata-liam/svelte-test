<script>
  import { fade } from 'svelte/transition';
  let open = false;
  let active = false;
</script>

<main>
  <div class="relative inline-block text-left">
    <button class="inline-flex justify-center w-full rounded-md border border-gray-300 shadow-sm px-4 py-2 bg-white text-sm font-medium text-gray-700 hover:bg-gray-50 focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-100 focus:ring-indigo-500" on:click="{() => open = !open}">
      Options
      {#if open }
        <svg xmlns="http://www.w3.org/2000/svg" class="-mr-1 ml-2 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z" clip-rule="evenodd" />
        </svg>
      {:else}
        <svg xmlns="http://www.w3.org/2000/svg" class="-mr-1 ml-2 h-5 w-5" viewBox="0 0 20 20" fill="currentColor">
          <path fill-rule="evenodd" d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z" clip-rule="evenodd" />
        </svg>
      {/if}
    </button>
    {#if open }
      <div class="absolute" transition:fade="{{duration: 300 }}">
        <div class="right-0 mt-2 w-56 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 focus:outline-none">
          <div class="py-1">
            <div>
              <a href="/" class="{active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'} block px-4 py-2 text-sm">Account settings</a>
            </div>
            <div>
              <a href="/" class="{active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'} block px-4 py-2 text-sm">Support</a>
            </div>
            <div>
              <a href="/" class="{active ? 'bg-gray-100 text-gray-900' : 'text-gray-700'} block px-4 py-2 text-sm">License</a>
            </div>
            <form method="POST" action="#">
              <div>
                <button type="submit" class={active ? 'bg-gray-100 text-gray-900' : 'text-gray-700', 'block w-full text-left px-4 py-2 text-sm'}>
                  Sign out
                </button>
              </div>
            </form>
          </div>
        </div>
      </div>
    {/if}
  </div>
</main>