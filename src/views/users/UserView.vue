<script>
import axios from "axios";

export default {
  name: "UserView",
  data(){
    return{
      users:[]
    }
  },
  methods:{
    getUsers(){
      axios.get('http://localhost:8080/v1/users?detailed=true').then(res=>{
        console.log(res.data);
        this.users=res.data;
      }).catch(function (error){
        //error
      })
    },
    deleteById(userId){
      if(confirm('Are you sure?')){
        axios.delete(`http://localhost:8080/v1/users/${userId}`).then(res=>{
          this.getUsers();
        }).catch(function (error){
          //error
        })
      }
    }
  },
  mounted(){
    this.getUsers();
  }
}
</script>

<template>
  <h1 class="d-flex justify-content-between align-items-center">
    <span>List User</span>
    <RouterLink to="/users/create" class="btn btn-primary">
      Add Student
    </RouterLink>
  </h1>

  <table class="table" >
    <thead class="table-dark" >
    <tr>
      <th>Nro.</th>
      <th>User</th>
      <th>First Name</th>
      <th>Last Name</th>
      <th>Email</th>
      <th>Age</th>
      <th>Birth Day</th>
      <th>Actions</th>
    </tr>
    </thead>
    <tbody v-if="users.length > 0">
    <tr v-for="(user, index) in this.users" :key="index">
      <td>{{ index + 1 }}</td>
      <td>{{ user.userName}}</td>
      <td>{{ user.firstName }}</td>
      <td>{{ user.lastName }}</td>
      <td>{{ user.email }}</td>
      <td>{{ user.age }}</td>
      <td>{{ user.birthDay }}</td>
      <td>
        <RouterLink :to="{ path: '/users/' + user.id + '/edit' }" class="btn btn-success">
          Edit
        </RouterLink>
        <button type="button" @click="deleteById(user.id)" class="btn btn-danger">
          Delete
        </button>
      </td>
    </tr>
    </tbody>
  </table>
</template>

<style scoped>

</style>