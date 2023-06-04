<script lang="ts">
    import { createEventDispatcher } from 'svelte';

    export let itemName: string;

    const dispatch = createEventDispatcher();
    function addFn () {
        dispatch('add-evt');
    };

</script>

<div class="container">
    <input
        type="text"
        class=""
        bind:value={itemName}
        placeholder="Ingresa una tarea..."
    />
    <button on:click={() => addFn()}>Agregar</button>
</div>

<style>
.container {
    display: flex;
    
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
}
</style>