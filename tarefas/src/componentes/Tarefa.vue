<template>
  <div class="listas-grid">
    <template v-if="lista.length">
        <ListaDeTarefa v-for="(listas, i ) in lista" :key="listas.name"
        @tarefaDeletada="$emit('tarefaDeletada',i)"
        @escolherTarefa="$emit('escolherTarefa',i)"
        :listas="listas"
        >
           
        </ListaDeTarefa>
      
        <!-- <slot>
            <ListaDeTarefa/>
        </slot> -->
       
       
    </template>
    <p v-else class="no-listas">Sua vida está em dias :)</p>
  </div>
</template>

<script>
import ListaDeTarefa from './ListaDeTarefa.vue';

export default {
    components:{ListaDeTarefa},
     props:{
        lista:{type:Array,required:true}
     }
}
</script>

<style scoped>
    .listas-grid{
        display:flex;
        justify-content: center;
        flex-wrap: wrap;
        margin: 10px;
    }
    .no-listas{
       color:#aaa;
       font-size: 1.7rem;
    }
</style>