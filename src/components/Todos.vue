<template>
    <TodoItem v-for="todo in todos" v-bind:key="todo.id" v-bind:todoProps="todo" />
</template>

<script>
import { ref } from 'vue'
import TodoItem from './TodoItem'


export default {
    name: 'Todos',
    components: { TodoItem },
    setup() {
        const todos = ref([
            {
                id: 1,
                title: "Todo 1",
                completed: false
            },
            {
                id: 2,
                title: "Todo 2",
                completed: true
            },
            {
                id: 3,
                title: "Todo 3",
                completed: true
            }
        ])
        return {
            todos
        }
    }
}
</script>

<style>
</style>