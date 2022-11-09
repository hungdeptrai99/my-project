<template>
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
      <tBody v-for="(value, index) in data" :key="index">
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
export default {
  data() {
    return {
      data: null,
    };
  },
  mounted() {
    axios
      .get("https://636a6a2ec07d8f936d9d24df.mockapi.io/APIlogin/user")
      .then((res) => {
        if (res.data) {
          this.data = res.data;
        }
      });
  },
};
</script>
