<template>
  <div class="inputBox shadow">
    <input type="text" v-model="newTodoItem" placeholder="Type what you have to do" v-on:keypress.enter="addTodo">
    <span class="addContainer" v-on:click="addTodo">
      <i class="addBtn fa fa-plus" aria-hidden="true"></i>
    </span>
 

  <modal v-if="showModal" @close = "showModal=false">
    <h3 slot = "header"> warning </h3> <!--modal header-->
    <span slot = "footer" @click = "showModal= false">
      please write Todo
      <i class = "closeModalBtn fa fa-times" aria-hidden="true"></i>
    </span>
  </modal>
   </div>
</template>

<script>
import Modal from './common/Modal.vue'

export default {
  data() {
    return {
      newTodoItem: '',
      showModal: false
    }
  },
  methods: {
    addTodo() {
      //console.log(this.newTodoItem); //this= the component App
      if (this.newTodoItem !== ""){
        var value = this.newTodoItem && this.newTodoItem.trim(); // remove the back and forth text in the input box
        this.$emit('addTodo', value);  // send event from Todoinput component to App component
        this.clearInput(); //initailize the input box input
      } else {
        this.showModal = !this.showModal;
      }
    },
    clearInput() {
      this.newTodoItem = '';
    },
    components: {
      Modal: Modal
    }
  }
};
</script>

<style scoped>
input:focus {
  outline: none;
}
.inputBox {
  background: white;
  height: 50px;
  line-height: 50px;
  border-radius: 5px;
}
.inputBox input {
  border-style: none;
  font-size: 0.9rem;
}
.addContainer {
  float: right;
  background: linear-gradient(to right, #6478FB, #8763FB);
  display: inline-block;
  width: 3rem;
  border-radius: 0 5px 5px 0;
}

.addBtn {
  color: white;
  vertical-align: middle;
}
</style>
