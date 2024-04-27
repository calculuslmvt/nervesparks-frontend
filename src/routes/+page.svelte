<script lang="ts">
    import { page } from '$app/stores';
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, GridSolid, MailBoxSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    $: activeUrl = $page.url.pathname;

	function handleClick(event : Event) {
        const target = event.target as HTMLInputElement;

		console.log(target.value); 
	}
</script>



<div class="bg-gray-900 top-0 left-0 w-full h-full fixed">
    
    <div class="flex flex-col relative justify-center items-center h-screen">
        <div class="text-slate-100 text-xl p-3">
            BuyCars 
        </div>
        <Sidebar {activeUrl}>
            <SidebarWrapper>
              <SidebarGroup>
                <SidebarItem label="Dealership" href="/dealership/login">
                  <svelte:fragment slot="icon">
                    <ChartPieSolid class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
                <SidebarItem label="Admin" href="/admin/login" active={activeUrl === '/docs/components/sidebar'}>
                  <svelte:fragment slot="icon">
                    <UserSolid class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
                <SidebarItem label="Log In" href="/user/login">
                  <svelte:fragment slot="icon">
                    <ArrowRightToBracketOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
                <SidebarItem label="Register" href="/user/register">
                  <svelte:fragment slot="icon">
                    <EditOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
              </SidebarGroup>
            </SidebarWrapper>
          </Sidebar>
    </div>
</div>


