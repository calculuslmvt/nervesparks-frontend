<script lang="ts">
    import axios from 'axios';
    // @ts-ignore
    import { Card, Button, Rating, Badge } from 'flowbite-svelte';
    import { onMount } from 'svelte';
    import { serverUrl } from '$lib/constants';
    import { searchValue } from '../stores';
    // @ts-ignore

    export let propValue: any ; 
    let carImage : any; 
    /**
     * @type {any[]}
     */
    let dealData: any[] = []; 
    
    let isLoading = true; 
    let isPurchasePrcessing = false; 
    let buyButton = "Buy"; 

    const handleSoldVehicle = async()=> {
        const url = serverUrl + '/user/sold-car-info';
        const response = await axios.post(url, {
            "soldVehicleId": propValue
        }, {withCredentials: true});  
        propValue = response.data.data;   
    };

    let carId = propValue?._id || "";
    onMount(async() => {

        await handleSoldVehicle();
        carImage = propValue?.car_info?.car_image || "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT3A6p6Odp1heDj1YSNFaeYtdwBvh3bwVYgXTNsdMNXTA&s";

        carId = await propValue?._id; 
        console.log(carId); 
        const url = serverUrl + '/user/get-deals-car';
        const response = await axios.post(url, {
            "car_id": carId
        }, {withCredentials: true});
        dealData = response.data.data;
        isLoading = false; 
        console.log("response"); 
        console.log(dealData);
    })

    // @ts-ignore
    const handleClick = async(deal)=> {
        // @ts-ignore
        try {
        isPurchasePrcessing = true; 
        const url = serverUrl + '/user/buy-car'; 
        const response = await axios.post(url, {
                            "car_id": carId,
                            "deal_id": deal._id
                        }, {withCredentials: true} );

        console.log(response);
        isPurchasePrcessing = false;
        buyButton =  "Success";

        } catch (error) {
            buyButton = "Failed";
            isPurchasePrcessing = false;  
        }
    }



</script>


    
  <Card padding="none">
    <div class="grid grid-cols-3 max-w-none w-[75rem]">
        <div class="col-span-1">
        <a href="/">
            <img class=" max-w-[23rem] p-8 rounded-t-lg" src={carImage} alt="product 1" />
          </a>
          <div class="px-5 pb-5 w-full">
            <a href="/">
              <h5 class="text-xl font-semibold tracking-tight text-gray-900 w-full dark:text-white">{propValue?.name}</h5>
            </a>
            
          </div>
        </div>
        
          <div class="col-span-2 px-5 grid grid-rows-5 justify-between items-center w-full">
             {#if isLoading}
                    <div>
                        Loading deal....
                    </div>
                {/if} 
            
            {#each dealData as deal}
              <div class="w-full">
                  <div class="text-xl grid grid-cols-3 gap-3">
                      <div class="text-slate-300 flex items-center">
                          {deal.deal_info?.name}
                      </div>
                      <div class="text-white flex items-center justify-center">
                          Deal : ${deal.deal_info?.price}  
                      </div>
                      <div class="">
                          
                            {#if deal.deal_info?.isDealValid}
                            <Button on:click={() => handleClick(deal)}>
                                {buyButton}
                            </Button>   
                            {:else}
                            <div class="text-red-600">
                                Sold out 
                            </div>
                            {/if}
                        
                      </div>
                  </div>
              </div>
              {/each}
              {#if isPurchasePrcessing}
                <div class="text-green-400">
                        Transition in process.....
                </div>
              {/if}
            </div>   
    </div>
      
  </Card>
