<script>
    import { fly } from 'svelte/transition';
    let todoItem = '';
    let todoList = [];
    // add items from input field to array
    function addToList() {
        if (!todoItem) return;
        todoList = [...todoList, {
            text: todoItem,
            status: false
        }];
        todoItem = '';
    }
    // remove items from array
    function removeFromList(index) {
        todoList.splice(index, 1);
        todoList = todoList;
    }
</script>

<form on:submit|preventDefault={addToList}>
    <input bind:value={todoItem}>
</form>

<div>
<ol class="todo-list">
    {#each todoList as item, index}
    <li transition:fly="{{ y: 20, duration: 200 }}">
    <input bind:checked={item.status} class="checkbox" type="checkbox">
    <span class:checked={item.status}>{item.text}</span>
    <button class="delete" type="button" on:click={() => removeFromList(index)} ></button>
    </li>
    {/each}
</ol>
</div>

<style>
    div{
        width: 50%;
        left: 25%;
        position: fixed;
    }
    .todo-list {
        list-style: none;
    }
    .checked {
        text-decoration: line-through;
    }

    .todo-list {
        margin: 2em;
        list-style: none;
        background-color: #d6ff8f;
        word-wrap: break-word;
    }
    li:nth-child(even) {
        background-color: #abe841;
    }
</style>