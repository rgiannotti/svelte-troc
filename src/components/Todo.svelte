<script lang="ts">
    import '@fontsource/roboto';

    import Input from "./Input.svelte";
    import Item from "./Item.svelte";

    let items: any[] = [];
    let itemName = "";

    const handleAddItem = (event: any) => {
        let item = {
            name: itemName,
            updating: false,
            completed: false
        };
        if (items.some(item => item.updating)) {
            let index = items.map(item => item.updating).indexOf(true);
            items.splice(index, 1, item);
        }else {
            items.push(item);
        }
        items = items;
        itemName = "";
    };

    const handleDeleteItem = (event: any) => {
        const { index } = event.detail;
        items.splice(index, 1);
        items = items;
    };

    const handleUpdateItem = (event: any) => {
        const { item, index } = event.detail;
        itemName = item.name;
        items[index].updating = !item.updating;
    };
</script>

<div>
    <div class="container">
        <div class="row">
            <div class="col-lg-8 offset-lg-2">
                <Input bind:itemName={itemName} on:add-evt={handleAddItem} />
            </div>

            <div class="col-lg-6 offset-lg-3">
                {#if items.length === 0}
                    <div class="no-items">
                        No hay tareas para mostrar
                    </div>
                {/if}

                {#each items as item, i}
                    <Item item={item} index={i} on:delete-evt={handleDeleteItem} on:update-evt={handleUpdateItem} />
                {/each}
            </div>
        </div>
    </div>
</div>

<style>
.container {
    font-family: Roboto;
    margin: 20px auto;
    width: 700px;
    background: #fff;
    border-radius: 10px;
    padding: 20px;
    box-shadow: rgba(0, 0, 0, 0.15) 0px 5px 15px 0px;
}

.no-items {
    font-size: 18px;
    text-align: center;
    margin: 20px 0;
}

</style>
