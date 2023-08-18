<script>
    import Todo from "$lib/components/Todo.svelte";
    import RandomQuote from "$lib/components/RandomQuote.svelte";
    import BottomLinks from "$lib/components/BottomLinks.svelte";
</script>

<div class="w-4/5 mx-auto">
    <div class="grid gap-3 grid-cols-2">
        <Todo/>
        <section>
            <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:py-16 lg:px-12">
                <RandomQuote/>

            </div>
        </section>
    </div>
</div>
<BottomLinks/>






