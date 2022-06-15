<script setup>
import { auth } from "../firebase";
import { createUserWithEmailAndPassword } from "firebase/auth";
import UserForm from "../components/UserForm.vue";
</script>

<template>
  <div>
    <UserForm title="Register" @form-submit="formSubmit" />
  </div>
</template>

<script>
export default {
  name: "RegisterView",
  methods: {
    formSubmit(data) {
      const { email, password } = data;
      console.log("Register:", email, password);
    },
  },
};
</script>