<template>
  <form @submit.prevent="onSubmit">
    <h1>Login</h1>
    <p :style="{ color: 'red' }" v-if="error.status">
      {{ error.text }}
    </p>
    <p :style="{ color: 'red' }" v-if="success.status">{{ success.text }}</p>
    <div class="mb-3">
      <label for="username">User name</label>
      <input
        class="form-control w-200"
        :class="{ error: error.status }"
        type="text"
        v-model="form.userName"
        placeholder="Enter userName"
        id="username"
      />
    </div>
    <div class="mb-3">
      <label for="password">Password</label>
      <input
        class="form-control w-200"
        :class="{ error: error.status }"
        type="password"
        v-model="form.password"
        placeholder="Enter password"
        id="password"
      />
    </div>
    <button class="btn btn-success" type="submit">Login</button>
  </form>
</template>

<script>
import axios from "axios";
import { loginAPI } from "../api";
export default {
  // eslint-disable-next-line vue/multi-word-component-names
  name: "Login",
  data() {
    return {
      form: {
        userName: "",
        password: "",
      },
      error: {
        text: "",
        status: false,
      },
      success: {
        text: "",
        status: false,
      },
    };
  },
  methods: {
    async onSubmit() {
      if (this.form.userName.length < 6 || this.form.password.length < 6) {
        this.error = {
          text: "Bạn phải nhập hơn 6 kí tự",
          status: true,
        };
      } else {
        this.error = {
          text: "",
          status: false,
        };
      }
      let result = await axios.get(
        loginAPI(this.form.userName, this.form.password)
      );
      console.log(result)
      if (result.status == 200 && result.data.length > 0) {
        if (
          result.data[0].username === this.form.userName &&
          result.data[0].password === this.form.password
        ) {
          localStorage.setItem("user-info", JSON.stringify(result.data));
          this.$router.push("/");
          this.success = {
            text: "",
            status: false,
          };
        } else {
          this.success = {
            text: "Bạn nhập sai tài khoản và mật khẩu",
            status: true,
          };
        }
      } else {
        this.success = {
          text: "Bạn nhập sai tài khoản và mật khẩu",
          status: true,
        };
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
input.error {
  border-color: red;
}
</style>
