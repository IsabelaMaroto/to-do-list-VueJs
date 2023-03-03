<template>
  <header>
    <div>
      <img class="logo" src="./assets/logo.png"/>
    </div>
  </header>
  <div v-if="!editMode" class="list">
    <h2>Suas tarefas:</h2>
    <todo-list 
      v-bind:todos="todos" 
      @deleteTodo="deleteTodo" 
      @editTodo="editTodo"
    />
    <div class="button">
      <ButtonType @click="newTodo">Criar</ButtonType>
    </div>
  </div>
  
  <todo-item 
    v-if="editMode" 
    @cancel="cancel" 
    @saveTodo="saveTodo"
    v-bind:todo="todo"
  />

</template>

<script>
import TodoList from "./components/Todo-List.vue";
import TodoItem from "./components/Todo-Item.vue";

export default {
  components:{
    TodoList,
    TodoItem
  },


  data(){
    return{
      editMode: false,
      todos: [],
      todo: null,
      nextId: 1,
    }
  },


  methods:{
    newTodo(){
      this.todo = null;
      this.editMode = true;
    },
    cancel(){
      this.editMode = false;
    },
    saveTodo(todo){
      if(todo.id){
        //edicao
        const index = this.todos.findIndex((item) => item.id === todo.id)
        this.todos[index]= todo;
      } else{
        //inclusao
        todo = {id:this.nextId, ...todo};
        this.todos.push(todo);
        
        this.nextId++;
        localStorage.setItem("nextId", this.nextId);
      }

      localStorage.setItem("todos", JSON.stringify(this.todos));
      this.editMode = false;
    },
    deleteTodo(index){
      this.todos.splice(index, 1);
      localStorage.setItem("todos", JSON.stringify(this.todos))
    },
    editTodo(index){
      this.todo = this.todos[index];
      this.editMode = true;
    }

  },

  created(){
    const todos = localStorage.getItem("todos");
    if(todos){
      this.todos = JSON.parse(todos);
    }

    const nextId = localStorage.getItem("nextId");
    if(nextId){
      this.nextId = parseInt(nextId);
    }
  }


}
</script>

<style>
body{
  margin: 0;
  background-image: url('./assets/23761114_6865706.jpg');
  background-size: cover;
  background-repeat:repeat-y;
 
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  color: white ;
}
header{
  background-color: #0D89EC;
  padding: 0.3rem;

  border-bottom: 2px dashed #000000 ;
}
.logo{
  height: 4rem;
}
.list{
  background-color: #3b5f7c;
  width: 80%;
  min-height: 35rem;
  margin: 1rem auto;
  padding: 1rem 2rem;
  backdrop-filter: brightness(80%);
  border: 2px dashed #000000 ;
}
.button{
  display: flex;
  justify-content: end;
  padding: 1rem ;
}
</style>
