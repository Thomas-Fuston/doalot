<script>
  import Todos from './components/Todo.vue';
  import InputField from "./components/InputField.vue";
  import ErrorPanel from "./components/Error.vue";

  export default {
    components:{ Todos, InputField, ErrorPanel },
    data(){
      return{
        /*
         *  Fake data to show some Tasks
         */
        todos: [
          {id: 1, task: "Walk the Dog", done: false, },
          {id: 2, task: "Breakfast", done: false, },
          {id: 3, task: "Clean the Kitchen", done: false, }
        ],
        newTask: '',
        showError: false,
        errorMSG: ''
      }
    },
    methods: {
      addTask(){
        if (!this.newTask) {
          this.showError = true;
          this.errorMSG = "Please enter a new Task before Add!";
          setTimeout(() => this.showError = false, 3000)
          return
        }

        let task = {
          id: Math.floor(Math.random() * 1000000),
          task: this.newTask,
          done: false,
        }
        this.todos = [task, ...this.todos];
        this.newTask = '';

      },
      deleteTask(id){
        this.todos = this.todos.filter((todo) => {
          return todo.id != id
        })
      }
    }
  }
</script>


<template>
  <transition name="error">
    <ErrorPanel v-if="showError" :error="errorMSG"/>
  </transition>

  <div class="app-header">
    <h1>Do Alot!</h1>
    <p>Be Productive! Task after Task.</p>
  </div>

  <div v-if='todos.length'>
    <transition-group tag="div" name="todo" appear>
      <Todos
        v-for='todo in todos'
        :key='todo.id'
        :todo='todo'
        @delete='deleteTask'
        @done='todo.done=!todo.done'/>
    </transition-group>
  </div>

  <div v-else>
    <p class="empty-list">
      ... Oh no, there is nothing left todo! ...
    </p>
  </div>

  <form @submit.prevent="addTask" class="add-todo-form">
    <InputField
      v-model="newTask"
      label="Add a New Task"
      type="text" />
    <button class="button" type="submit">Add</button>
  </form>

  <small>created by Thomas Fuston using Vue3</small>
</template>


<style>
  .app-header{
    margin-bottom: 40px;
  }
  .empty-list{
  text-align:center;
  color: #8492a6;
  }
  .add-todo-form {
  text-align:center;
  margin-top: 40px;
  }
  .button{
  border: 1px solid #1f2d3d;
  background: #7e5bef;
  color: #fff;
  font-size: 16px;
  padding: 10px 40px;
  box-shadow: 2px 2px 0 0 rgba(0,0,0,0.8);
  cursor: pointer;
  }
  .button:hover{
    background: #a389f4;
  }
  .button:active{
    transform: translateX(2px) translateY(2px);
    box-shadow: 0 0 0 0 rgba(0,0,0,0.8);
  }

  /* Errorpanel animation */
  .error-enter-from,
  .error-leave-to{
    opacity:0;
    transform:translateY(-100px);
  }
  .error-leave-active{
    transition: all 0.3s ease;
  }
  .error-enter-active{
    animation: wobble 0.3s ease;
  }
  @keyframes wobble {
    0% { transform: translateY(-100px); opacity: 0 }
    50% { transform: translateY(0px); opacity: 1 }
    60% { transform: translateX(8px); opacity: 1 }
    70% { transform: translateX(-8px); opacity: 1 }
    80% { transform: translateX(4px); opacity: 1 }
    90% { transform: translateX(-4px); opacity: 1 }
    100% { transform: translateX(0px); opacity: 1 }
  }

  /* Todo animation */
  .todo-enter-from,
  .todo-leave-to {
    opacity: 0;
    transform: translateX(-100px);
  }
  .todo-enter-active,
  .todo-leave-active{
    transition: all 0.3s ease;
  }
  .todo-move{
    transition: all 0.3s ease;
  }
  .todo-leave-active{
    position: absolute;
  }
</style>
