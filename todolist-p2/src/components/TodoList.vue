<template>
    <table>
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
        <tr v-for="(todo, index) in todoListA" v-bind:key="'todo_' + todo.id">
          <td>{{ todo.id }}</td>
          <td v-if="todo.edit === false">{{ todo.todo }}</td>
          <td v-else><input type="text" v-model="editText" :placeholder="todo.todo" @keydown="editTodoText($event, index)"></td>
          <td @click="toggleStatus(index)">{{ todo.done }}</td>
          <td><button @click="editTodo(index)">EDIT</button></td>
          <td><button @click="deleteTodo(index)">DELETE</button></td>
        </tr>
      </tbody>
    </table>
</template>

<script>
export default{
    name: 'TodoList',
    props: {
        todoListA: {
            type:Array,
            default(){
                return[];
            }
        }
    },
    data(){
        return{
            editText:"",
    //   todoList:[
    //     {
    //       id: 1,
    //       todo: "vue",
    //       done: false,
    //       edit: false,
    //     },
    //     {
    //       id: 2,
    //       todo: "react",
    //       done: false,
    //       edit: false,
    //     },
    //     {
    //       id: 3,
    //       todo: "angular",
    //       done: false,
    //       edit: false,
    //     },
    //   ]
        }
    },
    methods:{
    toggleStatus(index){
      if(this.todoListA[index].done){
        this.todoListA[index].done = false;
      }
      else{
        this.todoListA[index].done = true;
      }
    },
    deleteTodo(index){
        console.log("child");
        this.$emit('delete-todo', index)
    //   this.todoListA.splice(index, 1);
    },
    editTodo(index){
      if(this.todoListA[index].edit){
        this.todoListA[index].edit = false;
      }else {
        this.todoListA[index].edit = true;
      }
    },
    editTodoText(e, index){
      if(e.keyCode === 13){
        this.todoListA[index].todo = this.editText;
        this.editTodo(index);
      }
    }
    }
}
</script>