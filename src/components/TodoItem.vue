<template>
    <li>
        <span v-bind:class="{done: todo.completed}">
            <input type="checkbox" v-on:change="$emit('change-todo', todo.id)">
            <strong>{{ index + 1 }}</strong>
            {{ todo.title.toUpperCase() }}
        </span>
        <button class="delete_btn" v-on:click="$emit('delete-todo', todo.id)">&times;</button>
    </li>
</template>

<script>
export default {
    name: "TodoItem",
    props: {
        todo: {
            type: Object,
            required: true
        },
        index: Number
    }
}
</script>

<style scoped>
    li {
        border: 1px solid black;
        display: flex;
        justify-content: space-between;
        padding: 0.5rem 2rem;
        margin-bottom: 1rem;
    }

    .delete_btn {
        width: 2em;
        height: 2em;
        background: red;
        border-radius: 50%;
        color: white;
        font-weight: bold;
    }

    input {
        margin-right: 1rem;
    }

    .done {
        text-decoration: line-through;
    }
</style>