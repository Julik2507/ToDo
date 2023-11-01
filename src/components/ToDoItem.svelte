<script>
    export let id;
    export let text;
    export let isDone;
    import { createEventDispatcher } from 'svelte';

    const dispatch = createEventDispatcher();
</script>


<div class="todo-list__item" class:todo-list__item-done={isDone}>
    <input class="todo-list__check" 
    type="checkbox" 
    on:change={dispatch('change', { id })} 
    checked={isDone} />
    <p class="todo-list__text">{text}</p>
    <button class="todo-list__btn" on:click={dispatch('remove', { id })}>Удалить</button>
    
</div>

<style>
    .todo-list__item {
        display: flex;
        align-items: center;
        justify-content: space-between;
        padding: 20px;
        background-color: rgb(240, 173, 173);
        border-radius: 15px;
    }

    .todo-list__text {
        flex-grow: 1;
    }

    .todo-list__btn {
        border: none;
        border-radius: 10px;
        background-color: rgb(159, 175, 175);
        padding: 10px;
        min-width: 80px;
    }
    
    .todo-list__item-done {
        background: rgb(113, 226, 113);
    }

    .todo-list__item-done .todo-list__text {
        text-decoration: line-through;
    }
</style>

