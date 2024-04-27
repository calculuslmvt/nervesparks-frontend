<script>
  import { Tabs, TabItem } from 'flowbite-svelte';
  import UserAllCars from './userAllCars.svelte';
  import MyCars from './myCars.svelte';
  import SearchBar from './searchBar.svelte';
</script>

<Tabs>
  <TabItem open title="All Cars">
    <p class="text-sm text-gray-500 dark:text-gray-400 ">
      <b>Cars:</b>
      <SearchBar/>
      <UserAllCars/>
    </p>
  </TabItem>
  <TabItem title="My Cars">
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>My cars:</b>
      <MyCars/>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </TabItem>
  <TabItem title="Deals">
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>Users:</b>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </TabItem>
  <TabItem title="Dont Click">
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>Dashboard:</b>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </TabItem>
  <TabItem disabled>
    <span slot="title" class="text-gray-400 dark:text-gray-500">More...</span>
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>Disabled:</b>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </TabItem>
</Tabs>