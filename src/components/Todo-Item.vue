<template>
    <div class="container">
        <h2 class="titulo">Adicione ou edite sua tarefa!</h2>
        <InputText v-model="description" class="input"/>
        <div class="div-botoes">
            <ButtonType @click="cancel" class="btn-voltar">Voltar</ButtonType>
            <ButtonType @click="saveTodo">Salvar</ButtonType>
        </div>
    </div>
    
</template>


<script>
export default {
    data(){
        return{
            description: ""
        }
    },
    props: {
        todo: Object,
    },
    created(){
        if(this.todo){
            this.description = this.todo.description;
        }
    },
    methods:{
        cancel(){
            this.$emit("cancel");
        },
        saveTodo(){
            this.$emit("saveTodo", {...this.todo, description: this.description})
        }
    }
}
</script>


<style scoped>
.container{
  background-color: #3b5f7c;
  width: 80%;
  min-height: 35rem;
  margin: 1rem auto;
  padding: 3rem 2rem;
  backdrop-filter: brightness(80%);
  border: 2px dashed #000000 ;
  text-align: center;
}
.titulo{
    margin-bottom: 4rem;
}
.input{
    width: 80%;
}
.div-botoes{
    margin-top: 1rem;
}
.btn-voltar{
    margin-right: 1rem;
}
</style>
