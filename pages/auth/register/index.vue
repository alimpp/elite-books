<script setup>
import { 
    validUsername, 
    validPassword , 
    validaRequired ,
    validConfirmPassword 
} 
from '@/utils/validate'

definePageMeta({
    layout: "auth",
});

const form = ref({
    firstName : '',
    lastName : '',
    username : '',
    password: '',
    confirmPassword: ''
})

const error = ref({
    firstName: {
        status: false , 
        message: ''
    },
    lastName: {
        status: false , 
        message: ''
    },
    username: {
        status: false , 
        message: ''
    },
    password: { 
        status: false , 
        message: ''
    },
    confirmPassword: {
        status: false , 
        message: ''
    }
})

const handleRegister = () => {
    let AccessToRegister = true
    if(!validaRequired(form.value.firstName)){
        AccessToRegister = false
        error.value.firstName.status = true
        error.value.firstName.message = 'First name can not be empty'
    } else {
        AccessToRegister = true
        error.value.firstName.status = false
        error.value.firstName.message = ''
    }
    if(!validaRequired(form.value.lastName)){
        AccessToRegister = false
        error.value.lastName.status = true
        error.value.lastName.message = 'Last name can not be empty'
    } else {
        AccessToRegister = true
        error.value.lastName.status = false
        error.value.lastName.message = ''
    }
    if(!validUsername(form.value.username)){
        AccessToRegister = false
        error.value.username.status = true
        error.value.username.message = 'Username should have minimum 5 characters'
    } else {
        AccessToRegister = true
        error.value.username.status = false
        error.value.username.message = ''
    }
    if(!validPassword(form.value.password)){
        AccessToRegister = false
        error.value.password.status = true
        error.value.password.message = 'Password should have minimum 8 characters'
    } else {
        AccessToRegister = true
        error.value.password.status = false
        error.value.password.message = ''
    }
    if(!validConfirmPassword(form.value.confirmPassword,form.value.password)){
        AccessToRegister = false
        error.value.confirmPassword.status = true
        error.value.confirmPassword.message = 'Confirm Password should be similar to the password'
    } else {
        AccessToRegister = true
        error.value.confirmPassword.status = false
        error.value.confirmPassword.message = ''
    }
}
</script>

<template>
    <div class="__application_animation">
        <div class="d-flex">
           <span class="app-font-size-18">
              Sign up with
           </span>
           <span class="px-2 app-font-size-18 app-font-weight-600 app-color-primary">
            Elite Books
           </span>
        </div>

       <div class="d-flex mt-5 w-100">
        <div class="w-100">
            <CoreInput
                label="First Name"
                v-model="form.firstName"
                :error="error.firstName.status"
                :messageError="error.firstName.message"
            />
        </div>
       </div>
       
       <div class="d-flex mt-2 w-100">
        <div class="w-100">
            <CoreInput
                label="Last Name"
                v-model="form.lastName"
                :error="error.lastName.status"
                :messageError="error.lastName.message"
            />
        </div>
       </div>

       <div class="d-flex mt-5 w-100">
        <div class="w-100">
            <CoreInput
                label="Username"
                v-model="form.username"
                :error="error.username.status"
                :messageError="error.username.message"
            />
        </div>
       </div>
       
       <div class="d-flex mt-2 w-100">
        <div class="w-100">
            <CoreInput
                label="Password"
                v-model="form.password"
                :error="error.password.status"
                :messageError="error.password.message"
            />
        </div>
       </div>
              
       <div class="d-flex mt-2 w-100">
        <div class="w-100">
            <CoreInput
                label="Confirm Password"
                v-model="form.confirmPassword"
                :error="error.confirmPassword.status"
                :messageError="error.confirmPassword.message"
            />
        </div>
       </div>



       <div class="d-flex mt-5">
            <CoreBtn 
                name="Create Account" 
                background="primary"  
                borderRadius="5px" 
                width="160px"
                height="32px"
                @click="handleRegister"
            />
            <div class="mx-2">
                <CoreBtn 
                    name="Sign in" 
                    background="outline-primary-hover"  
                    borderRadius="5px" 
                    width="80px"
                    height="32px"
                    @click="navigateTo('/auth/login')"
                />
            </div>
       </div>
       
    </div>
</template>