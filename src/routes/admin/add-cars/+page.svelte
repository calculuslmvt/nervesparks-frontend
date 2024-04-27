<script>
    import { serverUrl } from "$lib/constants";
    import axios from "axios";
    // @ts-ignore
    // @ts-ignore
    import { Input, Label } from "flowbite-svelte";
    import { Textarea } from 'flowbite-svelte';
    let textareaprops = {
        id: 'message',
        name: 'message',
        label: 'Your message',
        rows: 4,
        placeholder: "Enter Car-Json Data",
    };  
    let carData = "";
    let status = ""
    const handleClick = async ()=> {
        try {
            const carJsonData = JSON.parse(carData);
        const url = serverUrl + "/admin/add-cars";
        const response = await axios.post(url, carJsonData);
        // @ts-ignore
        status = response.data.message; 
        console.log(response);
        } catch (error) {
            // @ts-ignore
            status = error.message; 
        }
        
    }

</script>

<div class="bg-gray-900 top-0 left-0 w-full h-full fixed text-white">
    <div class="flex flex-col relative justify-center w-1/2 items-center h-screen">
        
        <div class="text-xl text-slate-400">
            Add Cars
        </div>
        
        <Textarea bind:value={carData} {...textareaprops } />
            <div class="py-4 text-slate-500">
                 Example    : 
                <br/>
                "car_id": "9",
                <br>
                "type": "Sedan",
                <br>
                "name": "Verna",
                <br>
                "model": "2021",
                <br>
                {"'car_info': {'carSold': 'false', 'car_image': 'Link'}"}    
            </div>
           
            <div class="py-5">
                <button 
                on:click={handleClick}
                class="flex p-1 bg-slate-600 rounded-md">
                    Submit 
                </button>
            </div>
            <div class="py-3 text-sm text-green-400">
                {status}
            </div>
                
        </div>

</div>
