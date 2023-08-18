<script>
    import {
        BottomNav,
        BottomNavItem,
        Button,
        Input,
        Modal, Select
    } from "flowbite-svelte";
    import {Icon} from "flowbite-svelte-icons";

    let links = localStorage.links ? JSON.parse(localStorage.links) : []

    let addModal = false;
    let icons = [
        {value: 'link-solid', name: 'General'},
        {value: 'exclamation-circle-solid', name: 'Important'},
        {value: 'cart-outline', name: 'Shopping'},
        {value: 'cash-outline', name: 'Finances'},
        {value: 'chart-line-up-solid', name: 'Data'},
        {value: 'brain-solid', name: 'Educational'},
        {value: 'newspaper-solid', name: 'News'},
    ]
    let newLink = {
        url: "",
        name: "",
        icon: "link-solid"
    }
    const saveNewLink = () => {
        links = [...links, newLink];
        localStorage.links = JSON.stringify(links);
        addModal = false
    };

    let linkToRemove = '';
    const removeLink = () => {
        links = links.filter(link => link.url !== linkToRemove);
        localStorage.links = JSON.stringify(links);
        addModal = false
    }
</script>

<Modal bind:open={addModal} title="Add or remove link">
    <form on:submit={saveNewLink}>
        <h3 class="text-lg mb-2">Add link</h3>
        <div class="grid gap-3">
            <Input bind:value={newLink.url} size="sm" placeholder="url" />
            <Input bind:value={newLink.name} size="sm" placeholder="name" />
            <Select bind:value={newLink.icon} items={icons}/>

            <Button type="submit">add</Button>
        </div>

    </form>
    <form on:submit={removeLink}>
        <h3 class="text-lg mb-2">Remove link</h3>
        <div class="grid gap-3">
            <Select bind:value={linkToRemove} >
                {#each links as link}
                    <option value={link.url}>{link.name}</option>
                {/each}
            </Select>
            <Button color="red" type="submit">remove</Button>
        </div>

    </form>

</Modal>

<BottomNav position="absolute" classInner="grid-cols-4" navType="border">

    {#each links as link}
        <BottomNavItem btnName={link.name}>
            <a href={link.url} target="_blank" rel="noreferrer noopener">
                <Icon name={link.icon} class="w-5 h-5 mb-1 text-gray-500 dark:text-gray-400 group-hover:text-primary-600 dark:group-hover:text-primary-500" />
            </a>
        </BottomNavItem>
    {/each}
    <BottomNavItem btnName="Quick Links" on:click={()=>addModal=true}>
        <div class="flex gap-2">
            <Icon  name="circle-plus-solid" class="w-3 mb-1 text-gray-500 dark:text-gray-400 group-hover:text-primary-600 dark:group-hover:text-primary-500" />
            <Icon name="trash-bin-solid" class="w-3 mb-1 text-gray-500 dark:text-gray-400 group-hover:text-primary-600 dark:group-hover:text-primary-500" />
        </div>

    </BottomNavItem>

</BottomNav>