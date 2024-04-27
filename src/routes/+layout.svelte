<script>
import "../app.pcss";
import { Navbar, NavBrand, NavLi, NavUl, NavHamburger } from 'flowbite-svelte';



</script>

<div class=" backdrop-blur-lg bg-gradient-to-r from-indigo-500 via-purple-500 to-pink-500 text-white/80 z-50 flex flex-row relative ">
    <Navbar  >
        <NavBrand href="/">
          <img src="https://w7.pngwing.com/pngs/168/648/png-transparent-globe-logo-abstract-logo-gemstone-globe-orange.png" class="me-3 h-6 sm:h-9" alt="Flowbite Logo" />
          <span class="self-center whitespace-nowrap text-xl font-semibold dark:text-white">BuyCars.com</span>
        </NavBrand>
        <NavHamburger  />
        <NavUl >
          <NavLi href="/">Home</NavLi>
          <NavLi href="/admin/login">Admin</NavLi>
          <NavLi href="/dealership/login">Dealership</NavLi>
          <NavLi href="/">Contact</NavLi>
        </NavUl>
      </Navbar>
</div>

<slot>
    <div class="text-white">
        slot
    </div>
</slot>