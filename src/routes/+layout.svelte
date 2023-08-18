<script>
  import "../app.postcss";
  import {DarkMode, Navbar, NavBrand, NavHamburger, NavLi, NavUl} from "flowbite-svelte";
  import {page} from "$app/stores";
  import {base} from "$app/paths";
</script>
<div class="p-3">
    <DarkMode size="lg"/>
</div>

<div class="mt-5 w-4/5 mx-auto">
<slot />
</div>
