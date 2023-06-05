<script lang="ts">
    import { createEventDispatcher } from 'svelte';

    export let itemName: string;
    export let itemUpdating: boolean;

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
        on:keydown={e => { if (e.key === 'Enter') { addFn(); } } }
        placeholder="Ingresa una tarea..."
    />
    <button on:click={() => addFn()}>{ itemUpdating ? 'Salvar' : 'Agregar' }</button>
</div>

<style>
.container {
    display: flex;
    
    justify-content: center;
    align-items: center;
    margin-bottom: 20px;
}
</style>