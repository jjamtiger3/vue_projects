<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo="addTodo"></TodoInput>
    <TodoList v-bind:propsdata="todoItems" @removeTodo="removeoTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue';
import TodoInput from './components/TodoInput.vue';
import TodoList from './components/TodoList.vue';
import TodoFooter from './components/TodoFooter.vue';

export default {
  data () {
    var todoItems = [];
    return { todoItems };
  },
  methods: {
    addTodo (todoItem) {
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
    removeoTodo (todoItem, index) {
      localStorage.removeItem(todoItem);
      thiis.todoItems.splice(index, 1);
    },
    clearAll () {
      localStorage.clear();
      this.todoItems = [];
    }
  },
  created () {
    var locLen = localStorage.length;
    if(locLen > 0) {
      for(var i = 0; i < locLen; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },
  components: {
    TodoHeader, TodoFooter, TodoList, TodoInput
  }
}
</script>

<style>
  body {
    text-align: center;
    background-color: #f6f6f8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0, 0, 0, 0.03);
  }
</style>
