<template>
    <input type="text" v-model="newTodoItem" @keydown="addTodo" :placeholder="placeholder"/>
</template>

<script>
export default {
    name: 'AddTodo',

    props:{
        placeholder:{
            type: String,
            default(){
                return "";
            },
        },
    },

    data(){
        return{
            newTodoItem:"",
        };
    },
    methods:{
    addTodo(e){
      if(e.keyCode === 13){
        let newTodoObj ={
          id: this.todoList[this.todoList.length-1].id + 1,
          todo: this.newTodoItem,
          isCompleted: false,
          isEdit: false,
        };

        this.todoList.push(newTodoObj);
        this.newTodoItem = ""
      }
    },
    }
}
</script>