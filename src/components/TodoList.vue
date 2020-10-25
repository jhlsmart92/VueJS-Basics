<template>
  <section>
    <ul>
      <li v-for="(todoItem, index) in todoItems" class= "shadow"> <!--show local history data on the vue-->
        <i class = "checkBtn fa fa-check" aria-hidden="true"> </i>
        {{todoItem}}
        <span class = "removeBtn" type="button" @click = "removeTodo(todoItem, index)">
          <i class ="fa fa-trash-o" aria-hidden = "true"></i>
        </span>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  data() {
    return{
      todoItems: []// storage for localstorage data
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
    removeTodo(todoItem,index) { // index is internally managed in the Vue system
      localStorage.removeItem(todoItem);
      this.todoItems.splice(index, 1); //splice is the internally given JS API removing the array factor according to the number
    }
  }
};
</script>

<style>
  ul {
    list-style-type: none;
    padding-left: 0px;
    margin-top: 0;
    text-align: left;
  }
  li {
    display: flex;
    min-height: 50px;
    height: 50px;
    line-height: 50px;
    margin: 0.5rem 0;
    padding: 0 0.9rem;
    background: white;
    border-radius: 5px;
  }
  .checkBtn {
    line-height: 45px;
    color: #62acde;
    margin-right: 5px;
  }
  .removeBtn {
    margin-left: auto;
    color: #de4343;
  }
  .list-enter-active, .list-leave-active {
    transition: all 1s;
  }
  .list-enter, .list-leave-to {
    opacity: 0;
    transform: translateY(30px);
  }
</style>
