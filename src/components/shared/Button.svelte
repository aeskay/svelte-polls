<script>
    export let type = 'primary';
    export let flat = false;
    export let inverse = false;
</script>

<button on:click class={type} class:flat={flat} class:inverse={inverse}>
    <slot></slot>
</button>

<style>
    button{
        border: 0;
        cursor: pointer;
        border-radius: 6px;
        padding: 8px 12px;
        font-weight: 500;
        box-shadow: 1px 2px 3px rgba(0,0,0,0.2);
    }
    .primary{
        background: #c41230;
        color: white;
    }
    .secondary{
        background: #45c496;
        color: white;
    }
    .flat{
        box-shadow: none;
    }
    .primary.inverse{
        color: #c41230;
        background: white;
        border: 2px solid #c41230;
    }
    .secondary.inverse{
        color: #45c496;
        background: white;
        border: 2px solid #45c496;
    }
</style>