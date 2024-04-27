<script lang="ts">
    import { serverUrl } from "$lib/constants";
    import axios from "axios";
    import { onMount } from "svelte";
    import UserCarsCard from "./userCarsCard.svelte";

    let spanClass = 'flex-1 ms-3 whitespace-nowrap';
    const url = serverUrl + "/user/view-all-cars";
    let isLoading = true ; 
    let fallBackData = "Page loading....";
    let carData: any = []; 

    interface CarInfo  {
        carSold: string,
        carImage: string
    }

    interface Car {
        name: string,
        car_info: CarInfo
    }

    onMount(async() => {
        try {
            isLoading = true; 
            axios.defaults.withCredentials = true;
            const response = await axios.post(url, {withCredentials: true}); 
            carData = response.data.data; 
            //console.log(carData); 
            isLoading = false; 
        } catch(error:any) {
            console.log(error.message); 
        }
    })
    console.log(carData); 

</script>

<div class="flex flex-cols flex-wrap gap-3 py-5 overflow-y-auto h-[35rem]">
    {#if isLoading}
        <div class="text-xl">
            Loading....
        </div>
    {/if}
    {#each carData as car }
        <div class="w-full">
           <UserCarsCard propValue = {car}/> 
        </div>
    {/each} 
</div>