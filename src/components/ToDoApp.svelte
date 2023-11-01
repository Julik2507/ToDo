<script>
	import ToDoItem from "./ToDoItem.svelte";
    import ToDoControls from "./ToDoControls.svelte";
	import { onMount } from "svelte";



    let items = [];
    let id = 0;
    
    onMount(() => { 
    if (localStorage.key('items')) {
        items = JSON.parse(localStorage.getItem('items'));
    }
    if (items.length) {
        items.forEach((i) => {
            if (id < i.id) {
                id = i.id;
            }
        });
        id++;
    }
    });

    function onChangeStatus(event) {
        const item = items.find((i) => i.id === event.detail.id);
        item.isDone = !item.isDone;
        items = items;
        localStorage.setItem('items', JSON.stringify(items));
    }

    function onAddItem(event) {
        const item = {
            id: id++,
            text: event.detail.text,
            isDone: false
        };
        items.push(item);
        items = items;
    }

    function onDeleteItem(event) {
        const idx = items.findIndex(i => i.id === event.detail.id);
        items.splice(idx, 1)
        items = items;
    }
</script>

<div class="todo-app">
    <ToDoControls on:add={onAddItem}/>
    <div class="todo-app__field">
        {#each items as item}
            <ToDoItem id={item.id} text={item.text} isDone={item.isDone} on:change={onChangeStatus} on:remove={onDeleteItem} />
        {/each}
    </div>
</div>

<style>
    .todo-app {
        background: grey;
        border-radius: 15px;
        width: 700px;
        height: 80%;
        padding: 40px 60px;
        display: flex;
        flex-direction: column;
        gap: 35px;
    }

    .todo-app__field {
        background: white;
        border-radius: 15px;
        display: flex;
        flex-direction: column;
        gap: 25px;
        padding: 20px;
        overflow: auto;
        flex-grow: 1;

        

    }
</style>