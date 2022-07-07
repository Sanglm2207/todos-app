<template>
  <p :class="[todo-item, todoProps.completed ? 'is-completed': '']">
    <input  class="form-check-input" type="checkbox" :checked="todoProps.completed"/>
    {{ todoProps.title }}
    <button type="button" class="btn btn-danger btn-del">Delete</button>
  </p>
</template>

<script>

export default {
    name: 'TodoItem',
    props: ['todoProps'],
   
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