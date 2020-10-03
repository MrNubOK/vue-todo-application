<template>
    <div>
        <AddTodoItem
            @add-todo="addTodoItem"
        />
        <hr>
        <select v-model="filter">
            <option>all</option>
            <option>completed</option>
            <option>not completed</option>
        </select>
        <Loader v-if="loading" />
        <TodoList
            v-else-if="filteredTodos.length"
            v-bind:todos="filteredTodos"
            v-on:change-todo="changeTodo"
            v-on:delete-todo="deleteTodo"
        />
        <p v-else>No todo items</p>

        <div>
            <router-link to="/">Home</router-link>
        </div>
    </div>
</template>

<script>
    import TodoList from '@/components/TodoList'
    import AddTodoItem from '@/components/AddTodoItem'
    import Loader from '@/components/Loader'
    export default {
        name: 'App',
        data() {
            return {
                todos: [],
                loading: true,
                filter: 'all'
            }
        },
        mounted() {
            fetch('https://jsonplaceholder.typicode.com/todos?_limit=7')
                .then(response => response.json())
                .then(json => {
                    this.todos = json
                    this.loading = false
                });
        },
        computed: {
            filteredTodos() {
                let list = [];

                if (this.filter == 'all') {
                    list = this.todos
                }
                else if (this.filter == 'completed') {
                    list = this.todos.filter(todo => todo.completed === true)
                }
                else if (this.filter == 'not completed') {
                    list = this.todos.filter(todo => todo.completed === false)
                }

                return list;
            }
        },
        methods: {
            changeTodo(id) {
                let reverse_val = !this.todos.find(todo => todo.id === id).completed;
                this.todos.find(todo => todo.id === id).completed = reverse_val;
            },
            deleteTodo(id) {
                this.todos = this.todos.filter(todo => todo.id !== id)
            },
            addTodoItem(item) {
                this.todos.push(item)
            },
        },
        components: {
            TodoList,
            AddTodoItem,
            Loader
        }
    }
</script>

<style>
    select {
        margin: 10px;
    }
</style>