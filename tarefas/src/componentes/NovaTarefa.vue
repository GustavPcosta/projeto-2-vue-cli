<template>
  <div class="tarefas">
    <input v-model="name" class="elemento" @keydown.enter="add" type="text" placeholder="Nova tarefa"/>
    <button class="elemento" @onclick="add">+</button>
  </div>
</template>

<script>
export default {
    data(){
        return{
            name:''
        }
    },
    methods: {
    add(){
        this.$emit('tarefaAddicionada',{name:this.name});
        this.name =''
    }
    },
}
</script>

<style scoped>
    .tarefas{
        margin: 45px;
    }
    .elemento{
        outline: none;
        font-size: 2rem ;
        border:1px solid #fff;
        padding:5px 10px 8px;
    }
    input.elemento{
        width: 500px;
        background: #fff2;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
        color:#fff;
    }

    button.elemento{
        border-left:none;
        background-color:#2196f3;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
        color:#fff;
    }
</style>