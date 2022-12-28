<template>
  <div id="app">
    <header>
      <h1>Minhas tarefas</h1>      
    </header>
      <task />
      
  </div>
</template>

<script>
import Task from './components/Task.vue';

export default{
  name: 'app',
  components: {
    Task
  } 
}
</script>

<style scoped>
  header{
    display: flex;
    justify-content: center;
    align-items: center;
    width: 100%;
    height: 80px;
    color: white;
  }
</style>
