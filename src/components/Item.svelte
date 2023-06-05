<script lang="ts">
    import { createEventDispatcher } from 'svelte';
    import DeleteIcon from './DeleteIcon.svelte';
    import EditIcon from './EditIcon.svelte';

    export let item: any;
    export let index: number;

    const dispatch = createEventDispatcher();
    function deleteFn () {
        dispatch('delete-evt', { index });
    };
    function updateFn () {
        dispatch('update-evt', { item, index });
    };
</script>

<article class={index%2 == 0 ? 'row-1' : 'row-2'} >
    <div style="margin-right: 10px;"><input type="checkbox" bind:checked={item.completed}></div>
    <!-- svelte-ignore a11y-click-events-have-key-events -->
    <div class={item.completed ? 'item-name completed' : 'item-name'} on:click={() => item.completed = !item.completed}>
        {item.name}
    </div>
    <div class="item-buttons">
        <button on:click={() => updateFn()} disabled={item.updating}><EditIcon /></button>
        <button on:click={() => deleteFn()} class="danger"><DeleteIcon /></button>
    </div>
</article>

<style>
    article {
        display: flex;
        align-items: center;
        padding: 5px 10px;
        border-radius: 10px;
    }
    button {
        border: none;
        background-color: transparent;
        display: flex;
    }
    .item-name {
        display: flex;
        flex: 1;
        justify-self: start;
        align-items: center;
        cursor: pointer;
    }
    .item-buttons {
        display: flex;
        justify-self: end;
        align-items: center;
    }
    .danger {
        color: red;
    }
    .row-1 {
        background-color: rgba(0, 0, 0, 0.05);
    }
    .row-2 {
        background-color: rgba(0, 0, 0, 0.025);
    }
    .completed {
        text-decoration: line-through;
    }
</style>