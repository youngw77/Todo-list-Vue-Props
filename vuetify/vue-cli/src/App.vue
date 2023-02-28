<template>
  <div id="app">
    <!-- 
      keyDown : 키보드가 눌리자마자
      keyUp : 키가 눌리는 진행중인 상태
      KeyPress : 키를 땠을 떄 특정키를 인식못함 옵션키
          -->
    <input type="text" v-model="newTodoItem" @keydown="addTodo"/>

    <v-simple-table dark>
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
          <td>{{ todo.todo }}</td>
          <td @click="toggleStatus(index)">{{ todo.isCompleted }}</td> 
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </v-simple-table>
  </div>
</template>

<script>
export default {
  name: 'App',

  data() {
    return {
      newTodoItem: "",

      todoList: [
      {
        id: 1,
        todo: 'Study Javascript',
        isCompleted: false,
      }, 
      {
        id: 2,
        todo: 'Do Homework',
        isCompleted: false,
      },
      {
        id: 3,
        todo: 'Take a shower',
        isCompleted: false,
      },
      {
        id: 4,
        todo: 'Brush Teeth',
        isCompleted: false,
      },
      {
        id: 5,
        todo: 'Talk to you',
        isCompleted: false,
      },
    ]
    }
  },
  methods: {
    toggleStatus(index){
      console.log("toggleStatus");

      // this.todoList[index].isCompleted =!this.todoList[index].isCompleted
      if(this.todoList[index].isCompleted) {
        this.todoList[index].isCompleted = false;
      } else{
        this.todoList[index].isCompleted = true;
      }
    },
    addTodo(e){
      console.log("addTodo", e);

      let length = this.todoList.length;
      console.log('length', length)

      if(e.keyCode === 13){
        let newTodoObj ={
          id: this.todoList[this.todoList.length-1].id + 1,
          // id: this.todoList.length + 1,
          todo: this.newTodoItem,
          isCompleted: false,
        };

        this.todoList.push(newTodoObj);
        this.newTodoItem = ""
      }
    },
    deleteTodo(index){
      console.log("deleteTodo", index);
      this.todoList.splice(index, 1);
    },

  },
};
</script>

<!-- <style>
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

</style> -->
