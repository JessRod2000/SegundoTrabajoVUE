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
      },
      validation: {
        userNameValid: true,
        emailValid: true,
        passwordValid: true,
        firstNameValid: true,
        lastNameValid: true,
        ageValid: true,
        birthDayValid: true,
        errorMessages: [],
      },
      resetValidation() {
        // Reset validation status and error messages
        for (const key in this.validation) {
          if (typeof this.validation[key] === "boolean") {
            this.validation[key] = true;
          } else if (Array.isArray(this.validation[key])) {
            this.validation[key].length = 0;
          }
        }
      }
    }
  },
  methods:{
    getUserById(userId){
      axios.get(`http://localhost:8080/v1/users/${userId}`).then(res=>{
        //console.log(res.data);
        this.model.user=res.data;
        //console.log(JSON.stringify(this.model.user, null, 2));
      }).catch(function (error){
        //error
      })
    },
    editUser(){
      if(this.validateForm()){
        axios.put(`http://localhost:8080/v1/users/${this.userId}`,this.model.user)
            .then(res=>{
              alert('Student was Edited sucessful');
            }).catch(function (error){
          //error
        })
      }else{

      }
    },
    validateForm() {
      const user = this.model.user;
      const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
      const textRegex = /^[a-zA-Z]+$/;
      const numberRegex = /^[0-9]+$/;
      const alphanumericRegex = /^[a-zA-Z0-9]+$/;

      // Reset validation status and error messages
      this.resetValidation();

      // Validate each field
      this.validateField("userName", alphanumericRegex.test(user.userName.trim()),"The userName field only alphanumeric characters are allowed.");
      this.validateField("email", emailRegex.test(user.email.trim()),"Please use the correct email format");
      this.validateField("password", user.password.trim() !== "", "The password field cannot be empty");
      this.validateField("firstName", textRegex.test(user.firstName.trim()),"The firstName field only allows alphabetic characters");
      this.validateField("lastName", textRegex.test(user.lastName.trim()),"The lastName field only allows alphabetic characters");
      this.validateField("age", numberRegex.test(user.age),"Invalid age");
      this.validateField("birthDay", user.birthDay.trim() !== "","The birthDay field cannot be empty");

      // Return true if all fields are valid, false otherwise
      return !this.validation.errorMessages.length;
    },
    validateField(fieldName, isValid,message) {
      // Set validation status for the field
      this.validation[fieldName + "Valid"] = isValid;

      // Add error message if the field is invalid
      if (!isValid) {
        this.validation.errorMessages.push(message);
      }
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
          <span v-if="!validation.userNameValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('userName')) }}
          </span>
        </div>
        <div class="mb-3">
          <label for="">Email</label>
          <input type="text" v-model="model.user.email" class="form-control">
          <span v-if="!validation.emailValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('email')) }}
          </span>
        </div>
        <div class="mb-3">
          <label for="">Password</label>
          <input type="text" v-model="model.user.password" class="form-control">
          <span v-if="!validation.passwordValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('password')) }}
          </span>
        </div>
        <div class="mb-3">
          <label for="">First Name</label>
          <input type="text" v-model="model.user.firstName" class="form-control">
          <span v-if="!validation.firstNameValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('firstName')) }}
          </span>
        </div>
        <div class="mb-3">
          <label for="">Last Name</label>
          <input type="text" v-model="model.user.lastName" class="form-control">
          <span v-if="!validation.lastNameValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('lastName')) }}
          </span>
        </div>
        <div class="mb-3">
          <label for="">Age</label>
          <input type="text" v-model="model.user.age" class="form-control">
          <span v-if="!validation.ageValid" class="error-message">
            {{ validation.errorMessages.find(message => message.includes('age')) }}
          </span>
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
