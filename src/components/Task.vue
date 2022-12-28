<template>
  <div id="task">

    <form @submit.prevent="addItem">
        <input 
          type="text"
          placeholder="Tarefa de hoje?"
          v-model="tarefa"
        />
        <button type="submit">Adicionar</button>
    </form>

    <Item :lista="tarefas" :delete="delTask"/>

    <span v-show="tarefas.length > 0">
      Você tem <strong :class="{pend: pendente}">{{ tarefas.length }}</strong> tarefas para realizar!
    </span>

  </div>
</template>

<script>
import Item from './Item.vue';

export default {
    name: 'Task',
    components:{
      Item,
    },
    data(){
      return{
        tarefa: '',
        tarefas: [],
        pendente: false
      }
    },
    methods:{
      addItem(){
        if(this.tarefa !== ''){
          this.tarefas.push({
            text: this.tarefa,
            key: Date.now(),
          });
        }else{
          alert('Digite uma tarefa');
          return;
        }
        this.tarefa = '';
  
      },
      delTask(key){
        let filtro = this.tarefas.filter( (item)=>{
          return (item.key !== key);
        });
          return this.tarefas = filtro;

      }
    },
    watch:{
      tarefas:{
        deep: true,
        handler(){
        localStorage.setItem('tasks', JSON.stringify(this.tarefas) );
        this.tarefas.length > 4 ?  this.pendente = true : this.pendente = false;
        }
      }
    },
    created(){
      const json = localStorage.getItem('tasks');
      this.tarefas = JSON.parse(json) || [];
    }
}
</script>

<style>
  #task{
    max-width: 700px;
    background: #fff;
    border-radius: 4px;
    padding: 20px;
    margin: 20px auto;
    box-shadow: 0 0 20px rbga(0,0,0, 0.3);
  }

  form{
    margin-top: 20px;
    display: flex;
    flex-direction: row;
  }

  form button {
    background: #0f5959;
    color: white;
    border: 0;
    border-radius: 4px;
    margin-left: 10px;
    padding: 0 15px;
    display: flex;
    justify-content: center;
    align-items: center;
  }

  input{
    flex: 1;
    border: 1px solid #eee;
    padding: 5px 10px;
    font-size: 14px;
    outline: none;
  }

  .pend{
    color: #e21102;
  }
</style>