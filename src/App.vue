<template>
  <div class="container">
    <h1 class="user_info">Users</h1>
    <table class="users-table">
      <thead>
        <tr>
          <th>Name</th>
          <th>Profile Picture</th>
          <th>Email</th>
          <th>Phone</th>
        </tr>
      </thead>
      <tbody>
        <tr @click="handleEdit(user)" v-for="(user, index) in users" :key="index">
          <td>{{ user.name }}</td>
          <td>
            <img :src="user.image" alt="User Image" class="profile-picture" />
          </td>
          <td>{{ user.email }}</td>
          <td>{{ user.phone }}</td>
        </tr>
      </tbody>
    </table>



    <div v-if="editUser" class="modal">
    <div class="modal-content">
      <span class="close-btn" @click="editUser = null">&times;</span>
      <h2>About User</h2>
      <img :src="editUser.image" alt="Profile Picture" class="modal-picture" />
      <p><strong>Name:</strong> {{ editUser.name }}</p>
      <p><strong>Email:</strong> {{ editUser.email }}</p>
      <p><strong>Phone:</strong> {{ editUser.phone }}</p>
      <p><strong>Company:</strong> {{ editUser.company.name }}</p>
    </div>
  </div>
    
  </div>
</template>

<script setup>

import { ref, onMounted, onUnmounted } from "vue";
import users from "./users.json";

const editUser = ref()

function handleEdit(item){
  console.log(item)
  editUser.value = item
}

function closeOnEscape(event) {
  if (event.key === "Escape") {
    editUser.value = null;
  }
}

onMounted(() => {
  window.addEventListener("keydown", closeOnEscape);
});

onUnmounted(() => {
  window.removeEventListener("keydown", closeOnEscape);
});


</script>

<style scoped>
.container {
  padding-right: 20px;
  padding-left: 20px;
  margin: 20px;
  font-family: Arial, sans-serif;
}
.user_info {
  color: #007bff;
}

h1 {
  text-align: center;
  margin-bottom: 20px;
}
.add-user-btn {
  display: block;
  margin: 0 auto 20px auto;
  padding: 10px 20px;
  font-size: 16px;
  color: #fff;
  background-color: #007bff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}
.users-table {
  width: 100%;
  border-collapse: collapse;
  margin: 0 auto;
}
.users-table th,
.users-table td {
  border: 1px solid #ddd;
  padding: 10px;
  text-align: center;
}
.profile-picture {
  width: 50px;
  height: 50px;
  border-radius: 50%;
}




.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal-content {
  
  background: #fff;
  padding: 20px;
  border-radius: 10px;
  max-width: 400px;
  width: 100%;
  text-align: center;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
  position: relative;

}

.modal-picture {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 20px;
  object-fit: cover;
}

.close-btn {
  position: absolute;
  top: 10px;
  right: 15px;
  font-size: 24px;
  font-weight: bold;
  color: #fff;
  background: none;
  background-color: #007bff;
  width: 25px;
  height: 30px;
  border-radius: 5px;
  border: none;
  cursor: pointer;
  transition: color 0.3s ease;
  z-index: 2000;
}

</style>
