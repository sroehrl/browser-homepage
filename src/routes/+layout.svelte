<script>
  import "../app.postcss";
  import {DarkMode} from "flowbite-svelte";
</script>
<div class="p-3">
    <DarkMode size="lg"/>
</div>

<div class="mt-5 w-4/5 mx-auto">
<slot />
</div>
