All-cars

<script lang="ts">
    import { serverUrl } from "$lib/constants";
    import axios from "axios";
    import { Sidebar, SidebarGroup, SidebarItem, SidebarWrapper, SidebarDropdownItem, SidebarDropdownWrapper } from 'flowbite-svelte';
    import { ChartPieSolid, GridSolid, CartSolid, MailBoxSolid, UserSolid, ArrowRightToBracketOutline, EditOutline } from 'flowbite-svelte-icons';
    import { onMount } from "svelte";
    let spanClass = 'flex-1 ms-3 whitespace-nowrap';

    const url = serverUrl + "/user/view-all-cars";
    let isLoading = true ; 
    let fallBackData = "Page loading....";


    onMount(async() => {
        try {

            isLoading = true; 
            axios.defaults.withCredentials = true;
            const response = await axios.post(url, {withCredentials: true}); 
            let carData = response.data.data; 
            console.log(carData); 
            isLoading = false; 
        } catch(error:any) {
            console.log(error.message); 
        }
    })
    
</script>

<div class="p-20">
    hi there
</div>