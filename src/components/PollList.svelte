<script>
// import { onDestroy, onMount } from "svelte";

//Using animations
import {fade, slide, scale} from 'svelte/transition';
import {flip} from 'svelte/animate';

import PollStore from "../stores/PollStore";
import PollDetails from "./PollDetails.svelte";

// export let polls = [];

// const unsub = PollStore.subscribe((data) => {
//     polls = data;
// });

// onMount(() => {
//     console.log('Mounted');
// })

// onDestroy(() => {
//     console.log("Destroyed")
//     unsub();
// });
    

</script>

<div class="poll-list">
    {#each $PollStore as poll (poll.id)}
        <div in:fade out:scale|local animate:flip={{duration: 500}}>
            <PollDetails {poll} on:vote/>

            <!-- Using on:vote alone above is called 'Event forwarding'
            This sends the event to the from the child of the present component to the parent of the present component-->
        </div>
    {/each}
</div>

<style>
    .poll-list{
        display: grid;
        grid-template-columns: 1fr 1fr;
        grid-gap: 20px;
    }
</style>