<script lang="ts">
    import { serverUrl } from "$lib/constants";
    import axios from "axios";
    import { onMount } from "svelte";
    import UserMyCarsCard from "./userMyCarsCard.svelte";

    interface CarInfo  {
            carSold: string,
            carImage: string
        }

    interface Car {
        name: string,
        car_info: CarInfo
    }

    const url = serverUrl + "/dealership/aboutme";
    let isLoading = true ; 
    let userData; 
    let vehicleInfo: any[] = []; 
    onMount(async() => {
        try {
            isLoading = true; 
            axios.defaults.withCredentials = true;
            const response = await axios.post(url, {withCredentials: true}); 
            userData = response.data?.data;
            vehicleInfo = userData?.sold_vehicles || [];  

            if(!vehicleInfo)return; 

            console.log("response");
            console.log(vehicleInfo); 

            isLoading = false; 
        } catch(error:any) {
            console.log(error.message); 
        }
    })

</script>

<div class="flex flex-cols flex-wrap gap-3 py-5 overflow-y-auto h-[35rem]">
    {#if isLoading}
        <div class="text-xl">
            Loading....
        </div>
    {/if}
    {#each vehicleInfo as soldCar }
        <div class="w-full">
           <UserMyCarsCard propValue = {soldCar}/> 
        </div>
    {/each} 
</div>