<script lang="ts">
    import {onMount} from "svelte";
    let quote = '';
    let author = '';

    onMount(async () => {
        // const res = await fetch('https://cors-anywhere.herokuapp.com/https://zenquotes.io/api/random/').then(res => res.json())
        const res = await fetch('https://zenquotes.io/api/random/').then(res => res.json())
        quote = res[0]['q']
        author = res[0]['a']
    })
</script>
<h1 class="mb-4 text-4xl font-extrabold tracking-tight leading-none text-gray-900 md:text-5xl lg:text-6xl dark:text-white">
    {quote}
</h1>
<p class="mb-8 text-lg font-normal text-gray-500 lg:text-xl sm:px-16 xl:px-48 dark:text-gray-400">{author}</p>
