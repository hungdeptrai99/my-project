<template>
  <div class="text-center">
    <router-link to="/login"> Login</router-link>
  </div>
  <h1>Welcome to page Home</h1>
  <div mb-8>
      <input
        class="form-control w-200"
        type="text"
        v-model="itemSearch"
        placeholder="Enter search"
        id="search"
      />
      <button class="btn btn-success mt-2" v-on:click="search">Search</button>
    <table v-if="flagSearch" class="table mb-">
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
    <div v-if="!flagSearch">Rất tiếc thứ mày search không có</div>
  </div>
</template>

<script>
import axios from "axios";
import { userAPI, searchAPI } from "../api";
export default {
  data() {
    return {
      data: null,
      itemSearch: null,
      flagSearch: true,
    };
  },
  methods: {},
  mounted() {
    axios.get(userAPI).then((res) => {
      if (res.data) {
        this.data = res.data;
      }
    });
  },
  computed: {
    search() {
      axios.get(searchAPI(this.itemSearch)).then((res) => {
        if (res.data.length > 0) {
          this.data = res.data;
          this.flagSearch = true;
        } else {
          this.flagSearch = false;
        }
      });
    },
  },
};
</script>
