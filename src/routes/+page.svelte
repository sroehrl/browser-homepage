<script>
    import Todo from "$lib/components/Todo.svelte";
    import RandomQuote from "$lib/components/RandomQuote.svelte";
    import BottomLinks from "$lib/components/BottomLinks.svelte";
    import {sineIn} from "svelte/easing";
    import {Drawer} from "flowbite-svelte";

    let transitionParamsRight = {
        x: 320,
        duration: 200,
        easing: sineIn
    };
    let hideDrawer = true;
</script>

<div >
    <div class="grid gap-2 grid-cols-2">
        <Todo/>
        <section>
            <div class="py-8 px-4 mx-auto max-w-screen-xl text-center lg:py-16 lg:px-12">
                <RandomQuote/>

            </div>
        </section>
    </div>
    <Drawer placement="right" transitionType="fly" transitionParams={transitionParamsRight} bind:hidden={hideDrawer} id="sidebar">

    </Drawer>
</div>
<BottomLinks/>






