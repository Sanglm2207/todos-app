<template>
    <AddTodo @add-todo="addTodo"/>
    <TodoItem 
        v-for="todo in todos" 
        :key="todo.id" 
        :todoProps="todo" 
        @item-completed="markComplete"
        @delete-item="deleteTodo"
        />
</template>

<script>
import { ref } from 'vue'
import axios from 'axios'

import TodoItem from './TodoItem'
import AddTodo from './AddTodo.vue'


export default {
    name: 'Todos',
    components: { TodoItem, AddTodo },
    setup() {
        const todos = ref([])

        const getAllTodos = async () => {
            try {
                const response = await axios.get('https://5ca73f878e58df0014602f41.mockapi.io/todos')
                console.log(response.data);
                todos.value = response.data
            } catch (error) {
                console.log(error);
            }
        }
        getAllTodos()

        const markComplete = id => {
            todos.value = todos.value.map(todo=> {
                if (todo.id === id) todo.completed = !todo.completed
                return todo
            })
        }

        const deleteTodo = async id => {
            try {
                await axios.delete(`https://5ca73f878e58df0014602f41.mockapi.io/todos/${id}`)
                todos.value = todos.value.filter(todo => todo.id !== id)
            } catch (error) {
                console.log(error);
                
            }
            
        }
        const addTodo = async newTodo => {
           try {
                const response = await axios.post('https://5ca73f878e58df0014602f41.mockapi.io/todos/', newTodo)
                todos.value.push(response.data)
           } catch (error) {
                console.log(error);
           }
            
        }
        return {
            todos,
            markComplete,
            deleteTodo,
            addTodo
        }
    }
}
</script>

<style>
</style>