<script lang="ts">
    import { serverUrl } from "$lib/constants";
    import axios from "axios";
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownItem, SidebarDropdownWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, GridSolid, CartSolid, MailBoxSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    import { onMount } from "svelte";
    import UserTabs from '$lib/components/userComponents/userTabs.svelte'

    let spanClass = 'flex-1 ms-3 whitespace-nowrap';

    let dealerships: any [] = []; 
    onMount(async()=> {
      const url = serverUrl + '/user/get-all-dealerships';
      const response = await axios.post(url,{withCredentials: true});
      dealerships = response.data?.data; 
      console.log("sidenav", dealerships);
    })


</script>
<slot>
</slot>
<div class="bg-gray-900 top-0 left-0 w-full h-full fixed text-white">
    <div class="grid grid-flow-row-dense grid-cols-4 h-full py-20 px-4">
        <div> 
            <Sidebar>
                <SidebarWrapper>
                  <SidebarGroup>
                    <SidebarItem href="all-cars" label="Dashboard">
                      <svelte:fragment slot="icon">
                        <ChartPieSolid class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                      </svelte:fragment>
                    </SidebarItem>
                    <SidebarDropdownWrapper label="Dealerships">
                      <svelte:fragment slot="icon">
                        <CartSolid class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                      </svelte:fragment>

                      {#each dealerships as dealer}
                        <SidebarDropdownItem label={dealer.dealership_name} />
                      {/each}
                    </SidebarDropdownWrapper>


                    <SidebarItem label="About Me">
                      <svelte:fragment slot="icon">
                        <UserSolid class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                      </svelte:fragment>
                    </SidebarItem>
                    <SidebarItem href = "/" label="Logout Out">
                      <svelte:fragment slot="icon">
                        <ArrowRightToBracketOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                      </svelte:fragment>
                    </SidebarItem>
                  </SidebarGroup>
                </SidebarWrapper>
              </Sidebar>
        </div>
        <div class =" col-span-3"> 
          <UserTabs/>
        </div>
    </div>
</div>