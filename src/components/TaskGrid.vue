<template>
  <div class="tasks">
      <Task v-for="(task, id) in tasks" v-bind:key='task.name'
      @taskDeleted="$emit('taskDeleted', id)" @taskState="$emit('taskState', i)" 
      v-bind:task="task" />
  </div>
</template>

<script>
import Task from './Task.vue'
export default {
    components: { Task },
    props: {
        tasks: { type: Array, required: true }
    }
}
</script>

<style>
    .tasks {
        display: flex;
        justify-content: center;
        flex-wrap: wrap;
    }

    .tasks .task{
        margin: 10px;
    }

</style>