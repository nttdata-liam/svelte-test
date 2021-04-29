<script>
  import { page } from '$app/stores';
  import { fade, slide } from 'svelte/transition';
  let active = false;

  const user = {
    name: 'Tom Cook',
    email: 'tom@example.com',
    imageUrl:
      'https://images.unsplash.com/photo-1472099645785-5658abf4ff4e?ixlib=rb-1.2.1&ixid=eyJhcHBfaWQiOjEyMDd9&auto=format&fit=facearea&facepad=2&w=256&h=256&q=80',
  }
  const navigation = [
    { name: 'Home', href: '/'},
    { name: 'About', href: '/about'},
    { name: 'TODOS', href: '/todos'},
    { name: 'Dropdown', href: '/dropdown'},
  ]

  let mobileNavOpen = false;
  let userNavigationOpen = false;
  const userNavigation = [
    { name: 'Your Profile', href: '#' },
    { name: 'Settings', href: '#' },
    { name: 'Sign out', href: '#' },
  ]
</script>

<main>
  <div as="header" class="bg-gray-800">
    <div class="max-w-7xl mx-auto px-2 sm:px-4 lg:divide-y lg:divide-gray-700 lg:px-8">
      <div class="relative h-16 flex justify-between">
        <div class="relative z-10 px-2 flex lg:px-0">
          <div class="flex-shrink-0 flex items-center">
            <img class="block h-8 w-auto" src="https://tailwindui.com/img/logos/workflow-mark-indigo-500.svg" alt="Workflow" />
          </div>
        </div>
        <div class="relative z-0 flex-1 px-2 flex items-center justify-center sm:absolute sm:inset-0">
          <div class="w-full sm:max-w-xs">
            <label for="search" class="sr-only">Search</label>
            <div class="relative">
              <div class="pointer-events-none absolute inset-y-0 left-0 pl-3 flex items-center">
                <svg xmlns="http://www.w3.org/2000/svg" class="h-5 w-5 text-gray-400" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                  <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z" />
                </svg>
              </div>
              <input id="search" name="search" class="block w-full bg-gray-700 border border-transparent rounded-md py-2 pl-10 pr-3 text-sm placeholder-gray-400 focus:outline-none focus:bg-white focus:border-white focus:ring-white focus:text-gray-900 focus:placeholder-gray-500 sm:text-sm" placeholder="Search" type="search" />
            </div>
          </div>
        </div>
        <div class="relative z-10 flex items-center lg:hidden">
          <!-- Mobile menu button -->
          <div class="rounded-md p-2 inline-flex items-center justify-center text-gray-400 hover:bg-gray-700 hover:text-white focus:outline-none focus:ring-2 focus:ring-inset focus:ring-white" on:click={() => mobileNavOpen = !mobileNavOpen}>
            <span class="sr-only">Open menu</span>
            {#if mobileNavOpen}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M10 14l2-2m0 0l2-2m-2 2l-2-2m2 2l2 2m7-2a9 9 0 11-18 0 9 9 0 0118 0z" />
              </svg>
            {:else}
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6 block" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M4 6h16M4 12h16M4 18h16" />
              </svg>
            {/if}
          </div>
        </div>
        <div class="hidden lg:relative lg:z-10 lg:ml-4 lg:flex lg:items-center">
          <button class="bg-gray-800 flex-shrink-0 rounded-full p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
            <span class="sr-only">View notifications</span>
            <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
            </svg>
          </button>

          <!-- Profile dropdown -->
          <div as="div" class="flex-shrink-0 relative ml-4">
            <div>
              <button class="bg-gray-800 rounded-full flex text-sm text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white" on:click="{(e) => userNavigationOpen = !userNavigationOpen}">
                <span class="sr-only">Open user menu</span>
                <img class="h-8 w-8 rounded-full" src={ user.imageUrl } alt="user headshot" />
              </button>
            </div>
            {#if userNavigationOpen}
              <div transition:fade="{{duration: 300 }}">
                <div class="origin-top-right absolute right-0 mt-2 w-48 rounded-md shadow-lg bg-white ring-1 ring-black ring-opacity-5 py-1 focus:outline-none">
                  {#each userNavigation as item}
                    <div>
                      <a href={ item.href } class="{active ? 'bg-gray-100' : ''} block py-2 px-4 text-sm text-gray-700">{ item.name }</a>
                    </div>
                  {/each}
                </div>
              </div>
            {/if}
          </div>
        </div>
      </div>
      <nav class="hidden lg:py-2 lg:flex lg:space-x-8" aria-label="Global">
        {#each navigation as item}
          <a  href={ item.href } class="rounded-md py-2 px-3 inline-flex items-center text-sm font-medium {$page.path == item.href ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white'}" aria-current={$page.path == item.href ? 'page' : undefined}>
            { item.name }
          </a>
        {/each}
      </nav>
    </div>

    {#if mobileNavOpen}
      <div as="nav" class="lg:hidden" aria-label="Global" transition:slide on:click={() => mobileNavOpen = !mobileNavOpen}>
          <div class="pt-2 pb-3 px-2 space-y-1">
            {#each navigation as item}
              <a href={item.href} class="block rounded-md py-2 px-3 text-base font-medium {$page.path === item.href ? 'bg-gray-900 text-white' : 'text-gray-300 hover:bg-gray-700 hover:text-white'}" aria-current={$page.path === item.href ? 'page' : undefined}>{ item.name }</a>
            {/each}
          </div>
        <div class="border-t border-gray-700 pt-4 pb-3">
          <div class="px-4 flex items-center">
            <div class="flex-shrink-0">
              <img class="h-10 w-10 rounded-full" src={user.imageUrl} alt="user headshot" />
            </div>
            <div class="ml-3">
              <div class="text-base font-medium text-white">{ user.name }</div>
              <div class="text-sm font-medium text-gray-400">{ user.email }</div>
            </div>
            <button class="ml-auto flex-shrink-0 bg-gray-800 rounded-full p-1 text-gray-400 hover:text-white focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-gray-800 focus:ring-white">
              <span class="sr-only">View notifications</span>
              <svg xmlns="http://www.w3.org/2000/svg" class="h-6 w-6" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 17h5l-1.405-1.405A2.032 2.032 0 0118 14.158V11a6.002 6.002 0 00-4-5.659V5a2 2 0 10-4 0v.341C7.67 6.165 6 8.388 6 11v3.159c0 .538-.214 1.055-.595 1.436L4 17h5m6 0v1a3 3 0 11-6 0v-1m6 0H9" />
              </svg>
            </button>
          </div>
          <div class="mt-3 px-2 space-y-1">
            {#each userNavigation as item }
              <a href={item.href} class="block rounded-md py-2 px-3 text-base font-medium text-gray-400 hover:bg-gray-700 hover:text-white">{ item.name }</a>
            {/each}
          </div>
        </div>
      </div>
    {/if}

  </div>
</main>