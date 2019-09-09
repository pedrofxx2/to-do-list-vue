<template>
  <div class="task" v-bind:class="stateClass">
      <span @click="$emit('taskDeleted', task)"  class="close">x</span>
      <p>{{ task.name }}</p>
  </div>
</template>

<script>
export default {
    props: {
        task: { type: Object, required: true }
    }, 
    computed: {
        stateClass() {
            return {
                pending: this.task.pending,
                done: !this.task.pending
            }
        }
    }, 
}
</script>

<style>
    .task {
        position: relative;
        box-sizing: border-box;
        width: 350px;
        height: 50px;
        padding: 8px;
        border-radius: 8px;
        font-size: 2rem;
        cursor: pointer;
        user-select: none;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .pending {
        border-left: 12px solid #b73229;
        background-color: #f44336;
    }

    .done {
        color: #DDD;
        border-left: 12px solid #0a8f08;
        background-color: #4caf50;
        text-decoration: line-through;
    }

    .pending .close{
        background-color: red;
    }

    .done .close{
        background-color: green;
    }

    .close {
        position: absolute;
        right: 1px;
        top: 15px;
        font-size: 1rem;
        font-weight: 600;
        height: 20px;
        width: 20px;
        border-radius: 10px;
        display: flex;
        justify-content: center;

    
    }
</style>