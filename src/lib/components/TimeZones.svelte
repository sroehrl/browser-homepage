<script lang="ts">
    import {onDestroy, onMount} from "svelte";
    import dayjs from "dayjs";
    import {Icon} from "flowbite-svelte-icons";
    import {Button, Modal, Select} from "flowbite-svelte";
    import utc from "dayjs/plugin/utc";
    import timezone from "dayjs/plugin/timezone";

    let availableTimezones: any[] = [];
    let times = localStorage.timeZones ? JSON.parse(localStorage.getItem('timeZones')) : [];
    let localTime = dayjs()
    let remoteTimes: any[] = [];
    let showPlanner = false;
    let ticker = setInterval(() => {
        localTime =localTime.add(1, 'second');
        remoteTimes.forEach(remoteTime => {
            remoteTime.time = remoteTime.time.add(1, 'second')
        })
        remoteTimes = [...remoteTimes]


    }, 1000)
    let open = false;

    let timeZoneToAdd: string;

    const addTimezone = (timezone: string) => {
        times = [...times, timezone];
        localStorage.setItem('timeZones', JSON.stringify(times))
        remoteTimes = [...remoteTimes, {
            time: dayjs().tz(timezone),
            tz: timezone
        }]
        open = false;
    }

    const getTimes = () => {
        times.forEach( (time:string) => {
            remoteTimes = [...remoteTimes, {
                time: dayjs().tz(time),
                tz: time
            }]
        })
    }

    const removeTimezone = (timezone: string) => {
        times = times.filter((time) => time !== timezone);
        localStorage.setItem('timeZones', JSON.stringify(times))
        remoteTimes = remoteTimes.filter((time) => time.tz !== timezone)
    }


    onDestroy(() => {
        clearInterval(ticker)
    })

    onMount(async () => {
        availableTimezones = await fetch('https://worldtimeapi.org/api/timezone').then(res => res.json())
        dayjs.extend(utc)
        dayjs.extend(timezone)
        getTimes();
    })
</script>
<div class="flex gap-3">
    <article class="p-3 bg-white/30 rounded-lg">
        <h3 class="text-white font-semibold">Local Time <Icon on:click={() => open = true   } name="plus-outline" class="w-2 inline cursor-pointer text-neutral-200"/></h3>
        <p class="text-white text-lg">{localTime.format('HH:mm')}<span class="text-sm">{localTime.format(':ss')}</span></p>
        {#if showPlanner}
            {#each {length: 23} as _,i}
                <p class="text-lg {i % 2 === 0 ? 'bg-white/80 text-neutral-600' : 'text-white'}">{localTime.add(i+1, 'hour').format('HH:mm')}</p>
            {/each}
        {/if}
    </article>
    {#each remoteTimes as time}
        <article class="p-3 bg-white/30 rounded-lg">
            <h3 class="text-white font-semibold">{time.tz} <Icon on:click={() => removeTimezone(time.tz)   } name="minus-outline" class="w-2 inline cursor-pointer text-neutral-200"/></h3>
            <p class="text-white text-lg">{time.time.format('HH:mm')}</p>
            {#if showPlanner}
                {#each {length: 23} as _,i}
                    <p class="text-lg {i % 2 === 0 ? 'bg-white/80 text-neutral-600' : 'text-white'}">{time.time.add(i+1, 'hour').format('HH:mm')}</p>
                {/each}
            {/if}
        </article>
    {/each}
    <div>
        <Icon name="clock-outline" class="w-8 cursor-pointer text-neutral-200" on:click={() => showPlanner = !showPlanner} />
    </div>
</div>
<Modal title="Available TimeZones" bind:open>
    <div class="flex gap-3">
        <Select bind:value={timeZoneToAdd} class="flex-1">
            {#each availableTimezones as timezone}
                <option value={timezone}>{timezone}</option>
            {/each}
        </Select>
        <Button on:click={() => addTimezone(timeZoneToAdd)}>add</Button>
    </div>
</Modal>
