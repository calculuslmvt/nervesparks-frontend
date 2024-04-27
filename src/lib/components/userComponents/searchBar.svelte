<script>
    import { Search, Button, Dropdown, DropdownItem } from 'flowbite-svelte';
    import { SearchOutline, ChevronDownOutline } from 'flowbite-svelte-icons';
    import { writable } from 'svelte/store';
    import {searchValue} from '../stores.js'

    const options = [
      {
        label: 'Dealers',
        labelSelected: 'Dealers',
        icon: '/images/forms/search-input/usa-flag.svg'
      },
      {
        label: 'Cars',
        labelSelected: 'Cars',
        icon: '/images/forms/search-input/de-flag.svg'
      },
      {
        label: 'Deals',
        labelSelected: 'Deals',
        icon: '/images/forms/search-input/it-flag.svg'
      }
    ]
      
    let textValue = ""; 
    const handleChange = ()=>{
        searchValue.set(textValue); 
        console.log(textValue); 
    }


    let selectOption = 'Cars'
    $: buttonLabel = options.find(({ labelSelected }) => labelSelected ===  selectOption)
  
  </script>
  
  <div class="p-2">
    <form class="flex">
    <div class="relative">
      <Button class="rounded-e-none whitespace-nowrap border border-e-0 border-primary-700 px-1">
        {buttonLabel?.labelSelected}
        <ChevronDownOutline class="w-2.5 h-2.5 ms-2.5" />
      </Button>
      <Dropdown classContainer="w-40">
        {#each options as option}
          <DropdownItem
            on:click={() => {
              selectOption = option.labelSelected;
            }}
            class="inline-flex items-center {selectOption === option.labelSelected ? 'underline' : ''}"
          >
            {option.label}
          </DropdownItem>
        {/each}
      </Dropdown>
    </div>
    <Search size="md" class="rounded-none py-2.5" bind:value={textValue} on:change={handleChange} placeholder="Search Cars, Deals and Dealerships... " />
    <Button class="!p-2.5 rounded-s-none">
      <SearchOutline class="w-6 h-6" />
    </Button>
  </form>
  </div>
