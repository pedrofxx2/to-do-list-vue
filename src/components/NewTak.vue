<template>
  <div class="new-task">
      <input type="text" v-model="name" @keydown.enter="add" 
            class="form-element" placeholder="Nova tarefa">
      <select v-model="points" class="form-element" @keydown.enter="add" >
          <option class="form-element" value="1">1</option>
          <option class="form-element" value="2">2</option>
          <option class="form-element" value="3">3</option>
          <option class="form-element" value="4">4</option>
          <option class="form-element" value="5">5</option>
          <option class="form-element" value="6">6</option>
          <option class="form-element" value="7">7</option>
          <option class="form-element" value="8">8</option>
          <option class="form-element" value="9">9</option>
          <option class="form-element" value="10">10</option>
          <option class="form-element" value="11">11</option>
          <option class="form-element" value="12">12</option>
          <option class="form-element" value="13">13</option>
      </select>  
      <button class="form-element" @click="add">+</button>
  </div>
</template>

<script>
export default {
    data() {
        return {
            name: '',
            points: 0
        }
    },
    methods: {
        add() {
            this.$emit('taskAdded', { name: this.name, points: this.points, day:this.day })
            this.name = ''
            this.points = 0
            this.day = 0
        }
    }
}
</script>

<style>
    .new-task {
        margin: 35px;
    }

    .form-element {
        outline: none;
        font-size: 2rem;
        border: 1px solid #FFF;
        padding:  5px 10px 8px;
        color: #FFF;
    }
    
    input.form-element {
        width: 500px;
        background: #FFF2;
        border-top-left-radius: 8px;
        border-bottom-left-radius: 8px;
    }

    select.form-element{
        width: 90px;
        background: #FFF2;
       
    }

    option.form-element {
        width: 50px;
        background: #FFF2;
         color: black;
       
    }


    button.form-element {
        border-left: none;
        background-color: cadetblue ;
        border-top-right-radius: 8px;
        border-bottom-right-radius: 8px;
    }

</style>