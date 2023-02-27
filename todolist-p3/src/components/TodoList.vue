<template>
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
          <td>{{ todo.todo }}</td>
          <td @click="toggleStatus(index)">{{ todo.isCompleted }}</td> 
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default {
    name:TodoList,
    data(){
        return{
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