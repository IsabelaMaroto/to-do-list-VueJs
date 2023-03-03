<template>
    <div class="todo-list">
        <div v-for="(todo, index) in todos" :key="index" class="todo-item">
                <CheckBox :inputId="todo.key" :value="todo.description" v-model="checked" class="checkBox"/>
                <label :for="todo.key" class="todo-label">{{ todo.description }}</label>
            <ButtonType 
                icon="pi pi-pencil" 
                class="p-button-rouded p-button-text"
                @click="$emit('editTodo', index)"
            ></ButtonType>
            <ButtonType 
                icon="pi pi-trash"
                class="p-button-rouded p-button-text" 
                @click="$emit('deleteTodo', index)"

                ></ButtonType>
        </div>
    </div>
    
</template>


<script>
export default {
    data(){
        return{
            checked: false
        }
    },
    props:{
        todos: Array
    },
}
</script>


<style scoped>
.todo-list{
    margin: 1rem;
}
.todo-item{
    display: flex;
    align-items: center;
    border-bottom: 1px dashed lightgray;
}
.todo-label{
    flex-grow: 1;
}
.checkBox{
    margin-right: 1rem;
}
</style>