<template>
	<div id="app">
		<h1>Tarefas</h1>
		<Progresso :progress="progress"/>
		<nova-tarefa @tarefaAddicionada="addTarefa"/>
		 <!-- <Tarefa v-for="listas of lista" :key="listas.name">
			<p>{{listas.name}}</p>  
		</Tarefa> -->
		<Tarefa
		:lista="lista"
		@tarefaDeletada="deletarTarefa"
		@escolherTarefa="alterarTarefa"
		>
		</Tarefa>
		
	</div>
</template>
<script>
import Progresso from './componentes/Progresso.vue';
import Tarefa from './componentes/Tarefa.vue';
import NovaTarefa from './componentes/NovaTarefa.vue';
export default {
	components:{Tarefa,NovaTarefa,Progresso},
	data(){
		return{
			lista:[
				
				{name:'Camiseta cara',pending:true},
				{name:'lavar prato',pending:false},			
			]
		}
	},
	methods: {
		addTarefa(task){
			const sameName = t => t.name === task.name
			const tarefaNova = this.lista.filter(sameName).length == 0;

			if(tarefaNova){
				this.lista.push({
					name:task.name,
					pending:task.pending || true
				})
				
			}
		},
		deletarTarefa(i){
			this.lista.splice(i,1)
			
		},
		alterarTarefa(i){
			this.lista[i].pending = !this.lista[i].pending
		}
	},

	computed:{
		progress(){
			const total = this.lista.length
			const acerto = this.lista.filter(t=>!t.pending).length

			return Math.round(acerto/total * 100 || 0)
		}
	},
	watch:{
		lista:{
			deep:true, //vai obeservar as mudanças de estados dentro do array
			handler(){
				localStorage.setItem('lista', JSON.stringify(this.lista))
			}
		}
	},
	created() {
		const json = localStorage.getItem('lista');
		this.lista = JSON.parse(json) || []
	},
}
</script>

<style>
	body {
		font-family: 'Lato', sans-serif;
		background: linear-gradient(to right, rgb(22, 34, 42), rgb(58, 96, 115));
		color: #FFF;
	}

	#app {
		display: flex;
		flex: 1;
		flex-direction: column;
		justify-content: center;
		align-items: center;
		height: 100vh;
	}

	#app h1 {
		margin-bottom: 5px;
		font-weight: 300;
		font-size: 3rem;
	}
</style>
