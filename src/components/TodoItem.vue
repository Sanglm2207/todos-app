<template>
  <p :class="[todo - item, todoProps.completed ? 'is-completed' : '']">
    <input class="form-check-input" type="checkbox" :checked="todoProps.completed" @change="markItemCompleted"  />
    {{ todoProps.title }}
    <button type="button" class="btn btn-danger btn-del" @click="deleteItem">Delete</button>
  </p>
</template>

<script>
// import { ref } from 'vue'

export default {
  name: 'TodoItem',
  props: ['todoProps'],
  setup(props, context) {
    const markItemCompleted = () => {
      context.emit('item-completed', props.todoProps.id)
    }

    const deleteItem = () => {
      context.emit('delete-item', props.todoProps.id)
    }
    return {
      markItemCompleted,
      deleteItem
    }
  }

}
</script>

<style>
.todo-item {
  background: #dba7a7;
  padding: 10px;
  margin: 0;
  border-bottom: 1px rgb(119, 119, 119) dotted;
}

.is-completed {
  text-decoration: line-through;
}

.btn-del {
  float: right;
}
</style>