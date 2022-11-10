<template>
  <div class="text-center">
    <router-link to="/login"> Login</router-link>
  </div>
  <h1>Welcome to page Home</h1>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th class="font-weight-bold text-danger">ID</th>
          <th class="font-weight-bold text-danger">USERNAME</th>
          <th class="font-weight-bold text-danger">PASSWORD</th>
        </tr>
      </thead>
      <tBody v-for="(value, index) of data" :key="index">
        <tr>
          <th>
            {{ index + 1 }}
          </th>
          <td>
            {{ value.username }}
          </td>
          <td>
            {{ value.password }}
          </td>
        </tr>
      </tBody>
    </table>
  </div>
</template>

<script>
import axios from "axios";
import { user } from "../api";
export default {
  data() {
    return {
      data: null,
    };
  },
  mounted() {
    axios.get(user).then((res) => {
      if (res.data) {
        this.data = res.data;
      }
    });
  },
};
</script>
