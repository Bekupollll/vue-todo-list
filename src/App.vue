<template>
  <div class="container">
    <Header @btnclick="ToggleAddTasked" title="Task Tracker" :showAddTasks="showAddTasks" />
    <div v-show="showAddTasks">
      <AddTask @addTask="addtask"/>
    </div>
    <Tasks @togglereminder="toggleReminder" @deletetask="deleteTask" :tasks="tasks"/>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Tasks from './components/Tasks.vue'
import AddTask from './components/AddTask.vue' 
export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask
  },
  data(){
    return{
      tasks: [],
      showAddTasks: false,
    }
  },  

  methods:{
    ToggleAddTasked(){
      this.showAddTasks = !this.showAddTasks
    },
    addtask(task){
      this.tasks = [ ...this.tasks, task]
    },
    deleteTask(id){
      if (confirm('Are you sure?')){
        this.tasks = this.tasks.filter((task)=> task.id !== id)
      }
    },
    toggleReminder(id){
      console.log(id)
      this.tasks = this.tasks.map((task) => task.id == id ? {...task, reminder: !task.reminder } : task)
    },
    async fetchTasks(){
      const res = await fetch('http://localhost:3000/tasks')
      const data = await res.json()
      return data
    },
    async fetchTask(id){
      const res = await fetch(`http://localhost:3000/tasks/${id}`)
      const data = await res.json()
      return data
    }
  },  
  async created(){
    this.tasks = await this.fetchTasks()
  },
}
</script>
<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

*{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
body{
  font-family: 'Poppins',sans-serif;
}
.container{
  max-width: 500px;
  margin: 30px auto;
  overflow: hidden;
  min-height: 300px;
  padding: 30px;
  border-radius: 5px;
  border: 1px solid steelblue;
}
.btn{
  display: inline-block;
  color: #fff;
  border: none;
  padding: 10px 20px ;
  margin: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:hover{
  transform:scale(1.1);
  transition: 300ms;
  border-radius: 10px;
}
</style>
