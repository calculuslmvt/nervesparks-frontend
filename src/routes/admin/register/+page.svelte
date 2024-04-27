<script lang="ts">
    import { page } from '$app/stores';
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    import { Label, Input } from 'flowbite-svelte';
    import { serverUrl } from '$lib/constants';
    import axios from 'axios';
    import { goto } from '$app/navigation';
    $: activeUrl = $page.url.pathname;


    let adminEmail = "";
    let password = ""; 
    let isLoading = false; 
    let registerStatus = ""

    const handleRegister = async ()=> {
        isLoading = true; 
        const url = serverUrl + "/admin/register";
        const payload = {
            admin_email: adminEmail, 
            password: password
        }
        try{
            const response = await axios.post(url,payload);
            registerStatus = response.data?.message; 
            goto("/admin/login"); 
        } catch (error: any) {
            registerStatus = "Invalid Credentials";
            try {
                const errorMessage = error?.response.data?.match(/<pre>(.*?)<\/pre>/s)[1];
                registerStatus = errorMessage.split('<br>')[0];
            } catch (error) {
                console.log("error while parsing server response"); 
            }
        }  finally {
            isLoading = false; 
            adminEmail = "";
            password = "";
        }
    }
</script>

<div class="bg-gray-900 top-0 left-0 w-full h-full fixed">
    
    <div class="flex flex-col relative justify-center items-center h-screen">
        <div class="text-slate-100 text-xl p-3">
            Register Admin
        </div>
        <Sidebar {activeUrl}>
            <SidebarWrapper>
              <SidebarGroup>
                <Label for="email" class="block mb-2"></Label>
                <Input id="email" 
                    size="md" 
                    placeholder="User Email" 
                    bind:value={adminEmail}/>

                <Label for="password" class="block mb-2"></Label>
                <Input id="password" 
                    type="password"
                    size="md" 
                    placeholder="Password" 
                    bind:value={password}/>
                
                <SidebarItem 
                on:click={handleRegister}
                label="Register">
                <svelte:fragment slot="icon">
                    <EditOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                </svelte:fragment>
                </SidebarItem>
                <SidebarItem 
                label="Log In" href="/admin/login">
                  <svelte:fragment slot="icon">
                    <ArrowRightToBracketOutline class="w-6 h-6 text-gray-500 transition duration-75 dark:text-gray-400 group-hover:text-gray-900 dark:group-hover:text-white" />
                  </svelte:fragment>
                </SidebarItem>
              </SidebarGroup>
            </SidebarWrapper>
          </Sidebar>
          <div class="text-red-500/80 text-sm p-3">
            {registerStatus}
        </div>
        
        {#if isLoading}
            <div class="text-red-500/80 text-sm p-3">
                Loading.... 
            </div>
        {/if}

    </div>
</div>