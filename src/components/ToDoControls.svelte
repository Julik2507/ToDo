<script>
    import { createEventDispatcher } from 'svelte';
    const dispatch = createEventDispatcher();
    
    let inputValue = '';
    function onClick() {
        if(inputValue.length) {
            dispatch('add', {text: inputValue});
            inputValue = '';
        }
    }
</script>

<div class="todo-controls">
    <input class="todo-controls__input" type="text" bind:value={inputValue} />
    <button class="todo-controls__btn" on:click={onClick}>Добавить</button>
</div>

<style>
    .todo-controls {
        display: grid;
        grid-template-columns: 70% 30%;
    }

    .todo-controls__input {
        border: none;
        border-radius: 15px 0 0 15px;
        padding: 15px;
    }

    .todo-controls__btn {
        border: none;
        border-radius: 0 15px 15px 0;
        background-color: yellow;
    }
</style>