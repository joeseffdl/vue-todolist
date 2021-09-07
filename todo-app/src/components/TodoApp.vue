<template>
  <div class="container">
    <h2 class="text-center mt-5">My Vue Todo App</h2>
  

    <!-- Input -->
    <div class="d-flex">
      <input v-model="task" type="text" placeholder="Enter task" class="form-control">
      <button @click="submitTask" class="btn btn-warning rounded-0">
        <div class="text-center">
          <span class="fas fa-check">
          </span>
        </div></button>
      </div>

    <!-- Task table -->
    <table class="table table-bordered mt-5">
      <thead>
        <tr>
          <th scope="col">Task</th>
          <th scope="col">Status</th>
          <th scope="col" class="text-center">#</th>
          <th scope="col" class="text-center">#</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(task, index) in tasks" :key="index">
          <td style="width: 450px">
            <span :class="{'status-finished': task.status === 'finished'}" >
              {{task.name}}<!-- Where Input should go -->
            </span>
          </td> 
          <td style="width: 100px">
            <span @click="changeStatus(index)" class="pointer"
              :class="{'status-todo': task.status === 'to-do',
              'status-inprogress': task.status === 'in-progress',
              'status-done': task.status === 'finished' }"
            >
              {{ firstCharUpper(task.status)}}<!-- Where Status should go -->
            </span>
          <td>
            <div class="text-center" @click="editTask(index)">
              <span class="fas fa-pen"></span>
            </div>
          </td>
          <td>
            <div class="text-center" @click="deleteTask(index)">
              <span class="fas fa-trash"></span>
            </div>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },

  data(){
    return{
      task: '',
      tasks:[
        /* Empty Array */
      ],
      editedTask: null,
      availableStatuses: ['to-do', 'in-progress', 'finished'],  
    }
  },

  methods: {
    submitTask(){
      if(this.task.length === 0) return;
      
      if(this.editedTask === null){
        this.tasks.push({
          name: this.task,
          status: 'to-do'
        });
      }else{
        this.tasks[this.editedTask].name = this.task;
        this.editedTask = null;
      }
      this.task = ''; /* Empties the Input field after submitting a task*/
    },

    deleteTask(index){
      this.tasks.splice(index, 1);
    },

    editTask(index){
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },

    changeStatus(index){
      let newIndex = this.availableStatuses.indexOf(this.tasks[index].status);
      if(++newIndex > 2) newIndex = 0;
      this.tasks[index].status = this.availableStatuses[newIndex];
    },

    firstCharUpper(str){
      return str.charAt(0).toUpperCase() + str.slice(1);
    }
  }
}
</script>

<style scoped>

.pointer {
  cursor: pointer;
}

.status-finished{
  text-decoration: line-through;
}

.status-todo{
  color: red;
}

.status-inprogress{
  color: orange;
}

.status-done{
  color: green;
}

</style>
