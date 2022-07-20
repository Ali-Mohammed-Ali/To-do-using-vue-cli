<template>
  <div class="container">
    <h2 class="text-center mt-5">Todo App</h2>
    <!-- input -->
    <div class="d-flex">
      <input v-model="task" type="text" class="form-control" placeholder="Enter Task">
      <button @click="addTask" class="btn btn-warning rounded-0">Add</button>
    </div>
    <!-- tasks table  -->
    <table class="table table-bordered">
  <thead>
    <tr>
      <th scope="col">Tasks</th>
      <th scope="col">Status</th>
      <th scope="col" class="text-center">#</th>
      <th scope="col" class="text-center">#</th>
    </tr>
  </thead>
  <tbody>
    <tr v-for="(task, index) in tasks" :key="index">
      <th><span :class="{'finished': task.status === 'finished'}">{{task.name}}</span></th>
      <td><span :class="{'text-danger': this.status === 'to-do','text-warning': this.status === 'in-progress','text-success': this.status === 'finished'}" @click="changeStatus(index)" class="pointer">{{task.status}}</span></td>
      <td><div @click="editTask(index)" class="text-center"><span class="fa fa-pen"></span></div></td>
      <td><div @click="deleteTask(index)" class="text-center"><span class="fa fa-trash"></span></div></td>
    </tr>
  </tbody>
</table>
  </div>
</template>

<script>
export default {
  name: 'TodoApp',
  props: {
    msg: String
  },
  data(){
    return {
      task: '',
      editedTask: null,
      avilableStatus: ["to-do", "in-progress", "finished"],
      tasks: [
        {
          name: 'Steal banana from the store.',
          status: 'to-do'
        },
        {
          name: 'Eat 1kg chocolate in one hour.',
          status: 'in-progress'
        }
      ]
    }
  },
  methods: {
    addTask() {
      if(this.task.length === 0) {
        return;
      }else {
              if (this.editedTask === null ) {
                this.tasks.push({
                name: this.task,
                status: "to-do"
              });
              }else {
                this.tasks[this.editedTask].name = this.task;
                this.editedTask = null;
              }
      }
      this.task= '';

    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    },
    editTask(index) {
      this.task = this.tasks[index].name;
      this.editedTask = index;
    },
    changeStatus(index) {
      let newIndex = this.avilableStatus.indexOf(this.tasks[index].status);
      if (++newIndex > 2 ) newIndex = 0;
      this.tasks[index].status = this.avilableStatus[newIndex];
    }
  }
}
</script>
<style scoped>
.pointer {
  cursor: pointer;
}
.finished {
  text-decoration: line-through;
}
</style>


