<script>
    import axios from 'axios';
    // @ts-ignore
    import { Card, Button, Rating, Badge, Label, Input } from 'flowbite-svelte';
    import { onMount } from 'svelte';
    import { serverUrl } from '$lib/constants';
    // @ts-ignore
    import { BugSolid } from 'flowbite-svelte-icons';

    export let propValue ; 
    const carImage = propValue?.car_info?.car_image || "https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcT3A6p6Odp1heDj1YSNFaeYtdwBvh3bwVYgXTNsdMNXTA&s";
    let carId = propValue?._id || ""; 

    let dealPrice = ""

    console.log(carId); 
    /**
     * @type {any[]}
     */
    let dealData= []; 
    
    let isLoading = false; 
    let isPurchasePrcessing = false; 
    let dealButton = "Make Deal"; 
    // @ts-ignore
    const handleClick = async(deal)=> {
        // @ts-ignore
        try {
            isLoading = true
            isPurchasePrcessing = true; 
            const url = serverUrl + '/dealership/create-deal';
            
            const dealDetails = {
                "car_id": carId,
                "deal_info": {
                    "price": dealPrice
                }
            }

            const response = await axios.post(url, dealDetails, {withCredentials: true} );
            console.log(response);
            isPurchasePrcessing = false;
            dealButton =  "Success!";
            isLoading = false; 
            } catch (error) {
                dealButton = "Failed";
                isPurchasePrcessing = false; 
                console.log(error); 
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
                        Creating deal....
                    </div>
                {/if} 
                <div class="w-full">
                    <div class="text-xl grid grid-cols-3 gap-3">
                        <div class="text-white flex justify-center">
                          <Label for="email" class="block mb-2"></Label>
                          <Input id="email" 
                              size="md" 
                              type="number"
                              placeholder="Enter Deal Amount" 
                              bind:value={dealPrice}/>
                        </div>
                        <div class="">
                          <Button on:click={handleClick}>
                              {dealButton}
                          </Button> 
                        </div>
                    </div>
                </div>
            </div>   
    </div>
      
  </Card>