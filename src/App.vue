<template>
  <div id="app">
    <h1>To-Do List</h1>
    <input type="text" v-model="newTask" placeholder="Tambah tugas baru">
    <button @click="addTask">Tambah</button>
    
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        <input type="checkbox" v-model="task.completed">
        <span :class="{ 'completed': task.completed }">{{ task.name }}</span>
        <button @click="editTask(index)">Edit</button>
        <button @click="deleteTask(index)">Hapus</button>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      tasks: [
        { name: 'Belajar Vue.js', completed: false },
        { name: 'Makan siang', completed: true },
        { name: 'Beli bahan masakan', completed: false }
      ],
      newTask: ''
    }
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push({ name: this.newTask, completed: false });
        this.newTask = '';
      }
    },
    editTask(index) {
      const newName = prompt('Masukkan nama tugas baru:', this.tasks[index].name);
      if (newName && newName.trim() !== '') {
        this.$set(this.tasks, index, { name: newName, completed: this.tasks[index].completed });
      }
    },
    deleteTask(index) {
      this.tasks.splice(index, 1);
    }
  }
}
</script>

<style scoped>
h1 {
    color: #343a40;
    text-align: center;
    margin-bottom: 20px;
    text-shadow: 2px 2px 4px rgba(0, 0, 0, 0.1);
  }
</style>
