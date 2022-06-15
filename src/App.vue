<script setup>
import { RouterLink, RouterView } from "vue-router";
import { auth, db } from "./firebase";
import { onAuthStateChanged, signOut } from "firebase/auth";
import { getDoc, doc } from "firebase/firestore";
</script>

<template>
  <div class="container pt-5">
    <header class="jumbotron">
      <h1>
        Hi
        <span class="badge badge-warning">{{ userDisplay }}</span>
        you are now in
        <span class="badge badge-primary">{{ $route.name }}</span>
        view.
      </h1>
      <h3>
        <router-link to="/login">Login</router-link> /
        <router-link to="/register">Register</router-link> /
        <router-link to="/">Home</router-link> /
        <a @click="onSignOutClick" href="#">Sign out</a>
      </h3>
    </header>
    <RouterView />
  </div>
</template>

<style lang="scss">
@import "./assets/style.scss";
a.router-link-active.router-link-exact-active {
  color: red;
}
</style>

<script>
export default {
  data() {
    return {
      isLogin: false,
      isAdmin: false,
      user: {
        email: "",
        uid: "",
      },
    };
  },
  computed: {
    userDisplay() {
      if (this.isLogin) {
        let name = this.user.email;
        if (this.isAdmin) {
          name += "[ADMIN]";
        }
        return name;
      } else {
        return "UNLOGIN USER";
      }
    },
  },
  methods: {
    onSignOutClick() {
      signOut(auth);
    },
  },
  mounted() {
    onAuthStateChanged(auth, (user) => {
      if (user) {
        console.log("user", user);
        //login...
        this.isLogin = true;
        this.user.email = user.email;
        this.user.uid = user.uid;
        getDoc(doc(db, "adminList/" + user.uid))
          .then((doc) => {
            console.log("doc", doc.exists());
            if (doc.exists()) {
              this.isAdmin = true;
            }
            this.checkLogin = true;
          })
          .catch((err) => console.log("err", err));
      } else {
        //sign out...
        this.isLogin = false;
        this.isAdmin = false;
        this.user = { email: "" };
      }
      //console.log("user", user);
    });
  },
};
</script>
