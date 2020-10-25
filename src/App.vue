<template>
  <div id="app">
    <TodoHeader></TodoHeader>
    <TodoInput v-on:addTodo = "addTodo"></TodoInput>
    <TodoList v-bind:propsdata = "todoItems" @removeTodo= "removeTodo"></TodoList>
    <TodoFooter v-on:removeAll="clearAll"></TodoFooter>
  </div>
</template>

<script>
import TodoHeader from "./components/TodoHeader.vue";
import TodoInput from "./components/TodoInput.vue";
import TodoList from "./components/TodoList.vue";
import TodoFooter from "./components/TodoFooter.vue";

export default {
  data() {
    return {
      todoItems: []
    }
  },

    // push all datas of the localhistory in to todoItems
  created() {  // after Vue instance created, move data from localhistory to vue data
    if(localStorage.length > 0) {
      for(var i = 0; i < localStorage.length; i++) {
        this.todoItems.push(localStorage.key(i));
      }
    }
  },

  methods: {
    addTodo(todoItem) { // add data to local history
      localStorage.setItem(todoItem, todoItem);
      this.todoItems.push(todoItem);
    },
  
    clearAll() {
      localStorage.clear();
      this.todoItems =[];
    },

    removeTodo(todoItem, index) { // revmoveTodo 함수 적는것 까먹었을때 왜 addTodo도 작동하지 않았는지?
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1);
    }
  },

  components: {
    TodoHeader: TodoHeader,
    TodoInput: TodoInput,
    TodoList: TodoList,
    TodoFooter: TodoFooter
  }
};
</script>

<style>
  body {
    text-align: center;
    background-color: #F6F6F8;
  }
  input {
    border-style: groove;
    width: 200px;
  }
  button {
    border-style: groove;
  }
  .shadow {
    box-shadow: 5px 10px 10px rgba(0,0,0,0.03)
  }
</style>
