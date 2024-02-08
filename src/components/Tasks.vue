<template>
  <div v-for="task in tasks" :key="task.id">
    <task @togglereminder="$emit('togglereminder')" @deletetask="$emit('deletetask',task.id)" :task="task"/>
  </div>
</template>

<script>
import Task from './Task.vue'
export default {
  components: { Task },
  name: 'Tasks',
  props: {
    tasks:Array
  },
  emits:['deletetask','togglereminder']
}
</script>


<style>

</style>
