<template>
    <tr>
      <td :style="{ textDecoration: task.completed ? 'line-through' : 'none' }">{{ task.title }}</td>
      <td>{{ task.completed ? 'Selesai' : 'Belum Selesai' }}</td>
      <td>
        <button @click="toggleStatus">
          {{ task.completed ? 'Batal' : 'Selesai' }}
        </button>
        <button v-if="!task.completed" @click="deleteTask">Hapus</button>
      </td>
    </tr>
  </template>
  
  <script>
  import { defineComponent } from 'vue';
  
  export default defineComponent({
    props: ['task'],
    emits: ['cancel-task', 'complete-task', 'delete-task'], // Menambahkan event untuk menghapus
    methods: {
      toggleStatus() {
        if (this.task.completed) {
          this.$emit('cancel-task', this.task.id); // Jika selesai, kirim event untuk membatalkan
        } else {
          this.$emit('complete-task', this.task.id); // Jika belum selesai, kirim event untuk menyelesaikan
        }
      },
      deleteTask() {
        this.$emit('delete-task', this.task.id); // Memancarkan event untuk menghapus
      }
    }
  });
  </script>
  