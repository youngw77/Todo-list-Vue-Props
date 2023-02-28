<template>
  <div id="app">
    <!-- <input type="text" v-model="newTodoItem" @keydown="addTodo"/> -->
    <add-todo v-bind:placeholder="placeholder"></add-todo>
    <table>
      <thead>
        <tr>
          <th>NO.</th>
          <th>TODO</th>
          <th>DONE</th>
          <th>EDIT</th>
          <th>DELETE</th>
        </tr>
      </thead>
      <tbody>
        <!-- v-for="objectName in arrayName" v-bind:key="objectName.id" -->
        <!-- 테이블에서 반복문이 여러개인 경우 키값이 중복 될 수 있어 배열 값 'todo'+ 붙여주기 -->
        <!-- {{  }} 괄호가 한개이면 값을 String으로 인식하기 때문에 JS에서 괄호를 2개 써준다 -->
        <tr v-for="(todo, index) in todoList" :key="'todo_' + todo.id">
          <td>{{ todo.id }}</td>
          <td v-if="todo.isEdit === false">{{ todo.todo }}</td>
          <td v-else><input type="text" 
            v-bind:placeholder="todo.todo" 
            v-model="editTodoItem" 
            @keydown="editTodoText($event, index)"></td>
          <td @click="toggleStatus(index)">{{ todo.isCompleted }}</td> 
          <td><button @click="editTodo(index)">edit</button></td>
          <td><button @click="deleteTodo(index)">delete</button></td>
        </tr>
      </tbody>
    </table>
  </div>
</template>



<script>
import AddTodo from './components/AddTodo.vue'
export default {
  name: 'App',

  components: {
    AddTodo
  },

  data() {
    return {
      newTodoItem: "",
      editTodoItem: "",
      todoList: [
      {
        id: 1,
        todo: 'Study Javascript',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 2,
        todo: 'Do Homework',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 3,
        todo: 'Take a shower',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 4,
        todo: 'Brush Teeth',
        isCompleted: false,
        isEdit: false,
      },
      {
        id: 5,
        todo: 'Talk to you',
        isCompleted: false,
        isEdit: false,
      },
    ]
    }
  },
  methods: {
    toggleStatus(index){
      if(this.todoList[index].isCompleted) {
        this.todoList[index].isCompleted = false;
      } else{
        this.todoList[index].isCompleted = true;
      }
    },
    addTodo(e){
      if(e.keyCode === 13 && this.todoList.length>0){
        let newTodoObj ={
          id: this.todoList[this.todoList.length-1].id + 1,
          todo: this.newTodoItem,
          isCompleted: false,
          isEdit: false,
        };

        this.todoList.push(newTodoObj);
        this.newTodoItem = ""
      }
      else if(e.keyCode === 13 && this.todoList.length === 0){
        let newTodoObj ={
          id: 1,
          todo: this.newTodoItem,
          isCompleted: false,
          isEdit: false,
        }
        this.todoList.push(newTodoObj);
        this.newTodoItem = ""
      }
    },
    deleteTodo(index){
      this.todoList.splice(index, 1);
    },
    editTodo(index){
      if(this.todoList[index].isEdit){
        this.todoList[index].isEdit = false;
      }
      else{
        this.todoList[index].isEdit = true;
      }
    },
    editTodoText(e, index){
      if(e.keyCode === 13){
      this.todoList[index].todo = this.editTodoItem;
      this.editTodo(index);
      this.editTodoItem="";
      }
    }
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

table thead tr th{
  height: 30px;
  background-color: black;
  color: white;
}

table thead tr th:nth-child(2){
  width: 150px;
}

table tbody tr td{
  height: 30px;
}

/* odd even 홀짝 나누기 */
table tbody tr:nth-child(odd){
  background-color: #cccccc;
}

table tbody tr:hover{
  background-color: lightgreen;
  cursor: pointer;
}

</style>
