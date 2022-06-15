<script setup>
import { auth } from "../firebase";
import { signInWithEmailAndPassword } from "firebase/auth";
import UserForm from "../components/UserForm.vue";
</script>

<template>
  <div>
    <UserForm title="Login" @form-submit="formSubmit" />
  </div>
</template>

<script>
export default {
  name: "LoginView",
  methods: {
    formSubmit(data) {
      const { email, password } = data;
      console.log("Login:", email, password);
    },
  },
};
</script>