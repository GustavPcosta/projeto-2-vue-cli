<template>
  <div  @click="$emit('escolherTarefa',tarefa)">
    <p class="listagem"
   :class="definirClasse"
    >
    <span @click.stop="$emit('tarefaDeletada',tarefa)" class="close">X</span>
       {{listas.name}}
    </p>
  </div>
</template>

<script>
export default {
        props:{
            listas:{type:Object,required:true}
        },
    computed:{
        definirClasse(){
            return{
                pending: this.listas.pending,
                done: !this.listas.pending
            }
        }
    }
}
</script>

<style scoped>
    .listagem{
        position: relative;
        box-sizing: border-box;
        width: 350px;
        height: 150px;
        padding:10px;
        border-radius: 8px;
        font-size:2rem;
        font-weight: 300;
        cursor:pointer;
        user-select: none;
        justify-content: center;
        display: flex;
        align-items: center;
    }
    .pending{
        border-left: 12px solid #b73229;
        background-color:#f44336;
    }
    .done{
        border-left: 12px solid #1bc75a;
        background-color:#26c73b;
        text-decoration: line-through;
    }

    .pending .close{
        background: #b73219;
    }

    .done .close{
        background: #0a8f08;
    }

    .close{
    position: absolute;
    right: 10px;
    top:10px;
    font-size: 0.9rem;
    font-weight: 600;
    height: 20px;
    border-radius: 10px;
    display: flex;
    justify-content: center;
    }
</style>