<template>
    <form @submit.prevent="addItem">
        <input type="text" v-model="title">
        <button type="submit">Create</button>
    </form>
</template>

<script>
    export default {
        data() {
            return {
                title: ''
            }
        },
        methods: {
            addItem() {
                let title = this.title.trim()

                if (title) {
                    const newTodo = {
                        id: Date.now(),
                        title: title,
                        completed: false
                    }

                    this.$emit('add-todo', newTodo)
                    this.title = ''
                }
            }
        }
    }
</script>

<style scoped>
    form {
        display: flex;
    }

    input {
        width: 90%;
    }
</style>