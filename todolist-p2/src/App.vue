<template>
  <div id="app">
    <input type="text" v-model="newTodo" @keydown="addTodo">
    <!-- <add-todo v-bind:placeholder="placeholder" v-on:emit-add-todo="emitAddTodo"></add-todo> -->
    <todo-list :todo-list-a="todoList" v-on:delete-todo="deleteTodo"></todo-list>
    <!-- event를 emit할때는 반드시 v-on을 사용해 줘야 한다 -->
    <!-- html tag 에서는 대문자가 존재하지 않음 단어와 단언 연결 - 사용 -->
    <!-- <table>
      <thead>
        <tr>
          <th>NO</th>
          <th>TODO</th>
          <th>DONE</th>
          <th>EDIT</th>
          <th>DELETE</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(todo, index) in todoList" v-bind:key="'todo_' + todo.id">
          <td>{{ todo.id }}</td>
          <td v-if="todo.edit === false">{{ todo.todo }}</td>
          <td v-else><input type="text" v-model="editText" :placeholder="todo.todo" @keydown="editTodoText($event, index)"></td>
          <td @click="toggleStatus(index)">{{ todo.done }}</td>
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </table> -->
  </div>
</template>

<script>
// import AddTodo from './components/AddTodo.vue';
import TodoList from "./components/TodoList.vue";
export default {
  name: 'App',

  components:{
    // AddTodo,
    TodoList,
  },

  data(){
    return{
      newTodo: "",
      editText:"",
      placeholder:"test",
      todoList:[
        {
          id: 1,
          todo: "vue",
          done: false,
          edit: false,
        },
        {
          id: 2,
          todo: "react",
          done: false,
          edit: false,
        },
        {
          id: 3,
          todo: "angular",
          done: false,
          edit: false,
        },
      ]
    }
  },
  methods:{
    emitAddTodo(data){
      data.id = this.todoList[this.todoList.length - 1].id +1;
      this.todoList.push(data);
    },
    addTodo(e){
      if(e.keyCode === 13){
        let newTodoObj ={
          id: this.todoList[this.todoList.length-1].id +1,
          todo: this.newTodo,
          done: false,
          edit: false,
        }
        this.todoList.push(newTodoObj);
        this.newTodo="";
      }
    },
    toggleStatus(index){
      if(this.todoList[index].done){
        this.todoList[index].done = false;
      }
      else{
        this.todoList[index].done = true;
      }
    },
    deleteTodo(index){
      console.log('-------')
      this.todoList.splice(index, 1);
    },
    editTodo(index){
      if(this.todoList[index].edit){
        this.todoList[index].edit = false;
      }else {
        this.todoList[index].edit = true;
      }
    },
    editTodoText(e, index){
      if(e.keyCode === 13){
        this.todoList[index].todo = this.editText;
        this.editTodo(index);
      }
    }
  }
}
</script>

<style>
thead tr th{
  background-color:black;
  color:white;
}

tbody tr:nth-child(odd){
  background-color: rgb(154, 228, 173);
}
</style>
