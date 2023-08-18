<script>
  import "../app.postcss";
  import {DarkMode, Navbar, NavBrand, NavHamburger, NavLi, NavUl} from "flowbite-svelte";
  import {page} from "$app/stores";
  import {base} from "$app/paths";
</script>
<DarkMode/>

<div class="mt-5 w-4/5 mx-auto">
<slot />
</div>
<style>
    body{
        background-size: cover;
        background-repeat: no-repeat;
        background-image: url("lucas-calloch-P-yzuyWFEIk-unsplash.jpg");
    }
</style>