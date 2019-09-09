<template>
  <div id="app">
    <h1>To Do List</h1>
    <NewTask  @taskAdded="addTask" />
    <TaskGrid @taskDeleted="deleteTask" :tasks = tasks />
  </div>
</template>

<script>
import TaskGrid from './components/TaskGrid.vue'
import NewTask from './components/NewTak.vue'

export default {
  components: { TaskGrid, NewTask },
  data() {
        return {
            tasks: []
        }
    },
    methods: {
      addTask(task) {
        const sameName = t => t.name === task.name;
        const reallyNew = this.tasks.filter(sameName).length == 0;
        if(reallyNew) {
          this.tasks.push({
            name: task.name,
            pending: task.pending || true
          })
        }else {
          alert("Está tarefa já foi incluida, favor incluir uma tarefa diferente.")
        }
      },
      deleteTask(i) {
        this.tasks.splice(i, 1);
      }
    },
}
</script>

<style>
  body {
    font-family: 'Lucida Sans', 'Lucida Sans Regular', 'Lucida Grande', 'Lucida Sans Unicode', Geneva, Verdana, sans-serif;
    background: linear-gradient(to right, rgb(45, 80, 50), rgb(58, 80, 100)); 
    color: white
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
    font-weight: 200;
    font-size: 3rem;
  }
</style>