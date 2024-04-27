<script lang="ts">
    import { page } from '$app/stores';
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    import { Label, Input } from 'flowbite-svelte';
    import axios from 'axios';
    import {goto} from "$app/navigation"
    import { serverUrl } from '$lib/constants';

    $: activeUrl = $page.url.pathname;

    let dealershipEmail = "";
    let password = ""; 
    let loginStatus = ""; 
    let isLoading = false; 

     

    const handleLogin = async ()=> {

        isLoading = true; 
        const url = serverUrl + "/dealership/login";
        const payload = {
            dealership_email: dealershipEmail,
            password: password
        }
        try{
            const response = await axios.post(url,payload);
            loginStatus = response.data?.message; 
            goto("/dealership/cars/all-cars"); 
        } catch (error: any) {
            loginStatus = "Invalid Credentials";
            try {
                const errorMessage = error?.response.data?.match(/<pre>(.*?)<\/pre>/s)[1];
                loginStatus = errorMessage.split('<br>')[0];
            } catch (error) {
                console.log("error while parsing server response"); 
            }
        }  finally {
            isLoading = false; 
            dealershipEmail = "";
            password = "";
        }
    }
</script>

<div class="bg-gray-900 top-0 left-0 w-full h-full fixed">
    
    <div class="flex flex-col relative justify-center items-center h-screen">
        <div class="text-slate-100 text-xl p-3">
            Dealership User
        </div>
        <Sidebar {activeUrl}>
            <SidebarWrapper>
              <SidebarGroup>

                <Label for="email" class="block mb-2"></Label>
                <Input id="email" 
                    size="md" 
                    placeholder="dealership Email" 
                    bind:value={dealershipEmail}/>

                <Label for="password" class="block mb-2"></Label>
                <Input id="password" 
                    type="password"
                    size="md" 
                    placeholder="Password" 
                    bind:value={password}/>
                <SidebarItem 
                on:click={handleLogin}
                label="Log In">
                  <svelte:fragment slot="icon">
                    <ArrowRightToBracketOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
                <SidebarItem label="Register" href="/dealership/register">
                  <svelte:fragment slot="icon">
                    <EditOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
              </SidebarGroup>
            </SidebarWrapper>
          </Sidebar>
        <div class="text-red-500/80 text-sm p-3">
            {loginStatus}
        </div>
        
        {#if isLoading}
            <div class="text-red-500/80 text-sm p-3">
                Loading.... 
            </div>
        {/if}
    </div>
   
</div>