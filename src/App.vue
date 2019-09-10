<template>
  <div id="app">
    <h1>To Do List</h1>
    <p v-if="tasks.length === 0">Adicione uma tarefa para começar!</p>
    <p>obs: Não se pode incluir tarefas repetidas e as mesmas devem ter pontuações entre 1 e 13.</p>
    <TaskProgress :progress = "progress" />
    <h2 v-if="progress === 100">As Tarefas foram concluidas!</h2>
    <NewTask  @taskAdded="addTask" />
    <TaskGrid v-bind:tasks = "tasks" @taskDeleted="deleteTask" @taskStateChanged="toggleTaskState"  />
    <h2>Suas tarefas somam {{ totalPoints() }} pontos</h2>
  </div>
</template>

<script>
import TaskGrid from './components/TaskGrid'
import NewTask from './components/NewTak.vue'
import TaskProgress from './components/TaskProgress.vue'


export default {
  components: {  TaskGrid, NewTask, TaskProgress },
   data() {
        return {
          tasks: []
          // days: [
          //   monday= { tasks: [], points: 0 },
          //   tuesday= { tasks: [], points: 0 },
          //   wendnesday= { tasks: [], points: 0 },
          //   thuesday= { tasks: [], points: 0 },
          //   friday= { tasks: [], points: 0 },
          //   saturday= { tasks: [], points: 0 },
          //   sunday= { tasks: [], points: 0 }
          // ]
        }
    },
computed: {
      progress() {
        const total = this.tasks.length
        const done = this.tasks.filter( t => !t.pending).length
        const result = Math.round(done / total * 100) || 0
        return result
      }
    },
    watch: {
      tasks: {
        deep: true,
        handler() {
          localStorage.setItem('tasks', JSON.stringify(this.tasks))
        }
      }
    },
    methods: {
      totalPoints(points) {
        parseInt(points)
        points = 0
        for(let i = 0; this.tasks.length > i; i++){
          points = points + parseInt(this.tasks[i].points)
        }
        return points
      },
      addTask(task) {
       //let total = 0
        const sameName = t => t.name === task.name;      
        const reallyNew = this.tasks.filter(sameName).length == 0
        if(reallyNew && task.points != 0) {
          this.tasks.push({
            name: task.name,
            pending: task.pending || true,
            points: task.points
          })
        }else{
          alert("Não pode adicionar uma tarefa repetida e nem uma tarefa com valor 0")
        }
        // for(var i = 0; this.days.length > i; i++){
        //   total = this.days[i].points + task.points;
        //   if(total + task.points > 13){
        //     continue;
        //   }else {
        //     if(reallyNew && task.points != 0) {
        //       this.days[i.tasks.push({
        //         name: task.name,
        //         pending: task.pending || true,
        //         points: task.points
        //       })]
        //     }else{
        //       alert("Não pode adicionar uma tarefa repetida e nem uma tarefa com valor 0")
        //     }
        //   }
        // }  
      },
      deleteTask(i) {
        this.tasks.splice(i, 1);
      },

      toggleTaskState(i) {
        this.tasks[i].pending = !this.tasks[i].pending
      }
    },
    created() {
      const json = localStorage.getItem('tasks')
      this.tasks = JSON.parse(json) || []
    }
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