<template>
  <div id="app">
    <h1>To Do List</h1>
    
    <!-- Form untuk menambah tugas -->
    <form @submit.prevent="addTask">
      <input type="text" v-model="newTask" placeholder="Tambahkan tugas...">
      <button type="submit">Tambah</button>
    </form>
    
    <!-- Daftar tugas -->
    <ul>
      <li v-for="(task, index) in tasks" :key="index">
        {{ task }}
        <span>
          <button @click="editTask(index)">Edit</button>
          <button @click="deleteTask(index)">Hapus</button>
        </span>
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim() !== '') {
        this.tasks.push(this.newTask.trim());
        this.newTask = '';
      }
    },
    editTask(index) {
      let updatedTask = prompt('Edit tugas:', this.tasks[index]);
      if (updatedTask && updatedTask.trim() !== '') {
        this.$set(this.tasks, index, updatedTask.trim());
      }
    },
    deleteTask(index) {
      if (confirm('Apakah Anda yakin ingin menghapus tugas ini?')) {
        this.tasks.splice(index, 1);
      }
    }
  }
};
</script>

<style>
ul {
  list-style-type: none;
  padding: 0;
}
li {
  margin-bottom: 10px;
}
button {
  margin-left: 5px;
}
</style>
