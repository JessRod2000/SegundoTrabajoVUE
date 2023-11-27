<script>
import axios from "axios";

export default {
  name: "UserEditView",
  data(){
    return{
      userId:'',
      model:{
        user:{
          userName: '',
          password:'',
          email: '',
          createdAt:'',
          userDetailId:'',
          firstName: '',
          lastName: '',
          age: '',
          birthDay: ''
        }
      }
    }
  },
  methods:{
    getUserById(userId){
      axios.get(`http://localhost:8080/v1/users/${userId}`).then(res=>{
        console.log(res.data);
        this.model.user=res.data;
        console.log(JSON.stringify(this.model.user, null, 2));
      }).catch(function (error){
        //error
      })
    },
    editUser(){
      axios.put(`http://localhost:8080/v1/users/${this.userId}`,this.model.user)
          .then(res=>{
            alert('Student was Edited sucessful');
          }).catch(function (error){
            //error
      })
    }
  },
  mounted() {
    this.userId=this.$route.params.id;
    this.getUserById(this.userId);
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header" style="background-color: #000000; color:#ffffff">
        <h4>Edit Users</h4>
      </div>
      <div class="card-body">
        <div class="mb-3">
          <label for="">UserName</label>
          <input type="text" v-model="model.user.userName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input type="text" v-model="model.user.email" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Password</label>
          <input type="text" v-model="model.user.password" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">First Name</label>
          <input type="text" v-model="model.user.firstName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.user.lastName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Birthday</label>
          <input type="date" v-model="model.user.birthDay" class="form-control">
        </div>

        <div class="d-flex justify-content-center mb-4">
          <button type="button" @click="editUser" class="btn btn-primary"  style="background-color: #000000; color:#ffffff; border-color: #000000; min-width: 120px;">
            Save
          </button>&nbsp;
          <RouterLink to="/users" class="btn btn-primary" style="background-color: #000000; color:#ffffff; border-color: #000000; min-width: 120px;">
            Back
          </RouterLink>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>