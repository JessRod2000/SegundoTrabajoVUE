<script>
import axios from "axios";

export default {
  name: "UserCreateView",
  data(){
    return{
      model:{
        user:{
          userName: '',
          password:'',
          email: '',
          createdAt:'',
          userDetail: {
            firstName: '',
            lastName: '',
            age: '',
            birthDay: ''
          }
        }
      }
    }
  },
  methods:{
    saveUser(){
      console.log(this.model.user);
      axios.post('http://localhost:8080/v1/users',this.model.user)
          .then(res=>{
            alert('User was saved');
            this.model.user={
              userName: '',
              password:'',
              email: '',
              createdAt: '',
              userDetail: {
                firstName: '',
                lastName: '',
                age: '',
                birthDay: ''
              }
            }
      }).catch(function (error){
        //error
      })
    }
  }
}
</script>

<template>
  <div class="container mt-5">
    <div class="card">
      <div class="card-header" style="background-color: #000000; color:#ffffff">
        <h4>Add Users</h4>
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
          <input type="text" v-model="model.user.userDetail.firstName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.user.userDetail.lastName" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.userDetail.age" class="form-control">
        </div>
        <div class="mb-3">
          <label for="">Birthday</label>
          <input type="date" v-model="model.user.userDetail.birthDay" class="form-control">
        </div>

        <div class="d-flex justify-content-center mb-4">
          <button type="button" @click="saveUser" class="btn btn-primary"  style="background-color: #000000; color:#ffffff; border-color: #000000; min-width: 120px;">
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