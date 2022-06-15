<template>
  <form @submit.prevent="formSubmit">
    <div class="form-group">
      <label for="email">Email</label>
      <input
        v-model="email"
        ref="email"
        type="email"
        class="form-control"
        required
      />
    </div>
    <div class="form-group">
      <label for="password">Password</label>
      <input
        v-model="password"
        ref="password"
        type="password"
        minlength="6"
        class="form-control"
        required
      />
    </div>
    <div class="form-group">
      <button class="btn btn-primary">{{ title }}</button>
    </div>
  </form>
</template>
<script>
export default {
  name: "UserForm",
  data() {
    return {
      email: "",
      password: "",
    };
  },
  props: ["title"],
  methods: {
    formSubmit() {
      this.$emit("form-submit", {
        email: this.email,
        password: this.password,
      });
    },
  },
};
</script>