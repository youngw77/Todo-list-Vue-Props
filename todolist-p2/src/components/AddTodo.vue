<template>
    <input type="text" v-model="newTodo" @keydown="addTodo" :placeholder="placeholder">
</template>

<script>
export default{
    name: 'AddTodo',

    props: {
        placeholder: {
            type: String,
            default() {
                return "";
            }
        }
    },
    data(){
        return{
            newTodo: "",
        }
    },
    methods:{
        addTodo(e){
      if(e.keyCode === 13){
        let newTodoObj ={
        //   id: this.todoList[this.todoList.length-1].id +1,
          todo: this.newTodo,
          done: false,
          edit: false,
        }
        // this.todoList.push(newTodoObj);
        console.log(newTodoObj);
        this.$emit('emit-add-todo', newTodoObj);
        this.newTodo="";
      }
    },
    }
}
</script>