<script>
    import axios from 'axios';
    // @ts-ignore
    import { Card, Button, Rating, Badge } from 'flowbite-svelte';
    import { onMount } from 'svelte';
    import { serverUrl } from '$lib/constants';
    // @ts-ignore
    import { BugSolid } from 'flowbite-svelte-icons';

    export let propValue ; 
    const carImage = propValue?.car_info?.car_image || "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT3A6p6Odp1heDj1YSNFaeYtdwBvh3bwVYgXTNsdMNXTA&s";
    let carId = propValue?._id || ""; 

    console.log(carId); 
    /**
     * @type {any[]}
     */
    let dealData= []; 
    
    let isLoading = true; 
    let isPurchasePrcessing = false; 
    let buyButton = "Buy"; 
    let success = ""; 
    onMount(async() => {
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
        success =  "Success";

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
              <h5 class="text-xl font-semibold tracking-tight text-gray-900 w-full dark:text-white">{propValue.name}</h5>
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
              <div class="text-green-400">
                {success}
              </div>
              
            </div>   
    </div>
      
  </Card>