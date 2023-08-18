<script lang="ts">
    import {Card, Checkbox, Heading, Input} from "flowbite-svelte";
    import {fade} from "svelte/transition";

    let todos = localStorage.todos ? JSON.parse(localStorage.todos) : [
        {done: false, text: "Todo 1"},
    ];
    let value = "";
    const checkTodo = (todo) => {
        if(todo.done){
            setTimeout(() => {
                todos = todos.filter((t) => t !== todo)
                localStorage.todos = JSON.stringify(todos)
            }, 1000)
        }
    }
    const add = (ev) => {
        todos = [...todos, {done: false, text: value}];
        localStorage.todos = JSON.stringify(todos);
        value = "";
        setTimeout(() => {
            ev.target.children[0].focus();
        },50)
    };
</script>
<div>
    <Heading tag="h2" class="mb-2">Todos</Heading>
    <Card>
        {#each todos as todo}
            <div transition:fade>
                <Checkbox bind:checked="{todo.done}" on:change={() => checkTodo(todo)}>
                    {todo.text}
                </Checkbox>
            </div>
        {/each}
        <form on:submit={add} class="{todos.length>0 ? 'mt-5' : ''}">
            <Input size="sm" placeholder="Add todo" bind:value/>
        </form>
    </Card>
</div>

