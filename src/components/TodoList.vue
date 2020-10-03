<template>
    <ul>
        <TodoItem
            v-for="(todo, i) of todos" :key="todo.id"
            v-bind:todo="todo"
            v-bind:index="i"
            v-on:change-todo="changeTodo"
            v-on:delete-todo="deleteTodo"
        />
    </ul>
</template>

<script>
import TodoItem from '@/components/TodoItem'
export default {
    props: ['todos'],
    components: {
        TodoItem
    },
    methods: {
        changeTodo(id) {
            this.$emit('change-todo', id)
        },
        deleteTodo(id) {
            this.$emit('delete-todo', id)
        }
    }
}
</script>

<style scoped>
    ul {
        list-style: none;
        margin: 0;
        padding: 0;
    }
</style>