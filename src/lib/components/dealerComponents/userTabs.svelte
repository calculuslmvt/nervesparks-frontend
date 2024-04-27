<script>
  import { Tabs, TabItem } from 'flowbite-svelte';
  import UserAllCars from './userAllCars.svelte';
  import MyCars from './myCars.svelte';
    import MyDeals from './myDeals.svelte';
</script>

<Tabs>
  <TabItem open title="All Cars">
    <p class="text-sm text-gray-500 dark:text-gray-400 ">
      <b>Cars:</b>
      <UserAllCars/>
    </p>
  </TabItem>
  <TabItem title="My Deals">
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>Users:</b>
      <MyDeals/>
      Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.
    </p>
  </TabItem>
  <TabItem title="Sold Cars">
    <p class="text-sm text-gray-500 dark:text-gray-400">
      <b>My cars:</b>
      <MyCars/>
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