<script lang="ts">
    import { page } from '$app/stores';
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    import { Label, Input } from 'flowbite-svelte';
    import { serverUrl } from '$lib/constants';
    import axios from 'axios';
    import { goto } from '$app/navigation';
    $: activeUrl = $page.url.pathname;

    let username =""
    let userEmail = "";
    let password = ""; 
    let userLocation = ""; 
    let isLoading = false; 
    let registerStatus = ""

    const handleRegister = async ()=> {
        isLoading = true; 
        const url = serverUrl + "/user/register";
        const payload = {
            user_email: userEmail,
            username: username,
            user_location: userLocation, 
            password: password
        }
        try{
            const response = await axios.post(url,payload);
            registerStatus = response.data?.message; 
            goto("/user/login"); 
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
            userEmail = "";
            password = "";
        }
    }
</script>

<div class="bg-gray-900 top-0 left-0 w-full h-full fixed">
    
    <div class="flex flex-col relative justify-center items-center h-screen">
        <div class="text-slate-100 text-xl p-3">
            Register User
        </div>
        <Sidebar {activeUrl}>
            <SidebarWrapper>
              <SidebarGroup>

                <Label for="username" class="block mb-2"></Label>
                <Input id="username" 
                    size="md" 
                    placeholder="Username" 
                    bind:value={username}/>

                <Label for="register-user-email" class="block mb-2"></Label>
                <Input id="register-user-email" 
                    size="md" 
                    placeholder="User Email" 
                    bind:value={userEmail}/>

                <Label for="user-location" class="block mb-2"></Label>
                <Input id="user-location" 
                    size="md" 
                    placeholder="Location" 
                    bind:value={userLocation}/>

                <Label for="register-user-password" class="block mb-2"></Label>
                <Input id="register-user-password" 
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
                label="Log In" href="/user/login">
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