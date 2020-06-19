<template>
  <div class="container py-5">
    <!-- AdminNav Component -->
    <AdminNav />
    <table class="table">
      <thead class="thead-dark">
        <tr>
          <th scope="col">#</th>
          <th scope="col">Email</th>
          <th scope="col">Role</th>
          <th scope="col" width="140">Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="user in users" :key="user.id">
          <th scope="row">{{user.id}}</th>
          <td>{{user.email}}</td>
          <td v-show="user.isAdmin">admin</td>
          <td v-show="!user.isAdmin">user</td>
          <td>
            <button
              v-show="!user.isAdmin"
              type="button"
              class="btn btn-link"
              @click.stop.prevent="toggleUserRole('user',user.id)"
            >set as admin</button>
            <button
              v-show="user.isAdmin"
              v-if="user.id !== currentUser.id"
              type="button"
              class="btn btn-link"
              @click.stop.prevent="toggleUserRole('admin',user.id)"
            >set as user</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import AdminNav from "../components/AdminNav";
import { mapState } from "vuex";
import adminAPI from "../apis/admin";
import { Toast } from "../utils/helpers";

export default {
  name: "AdminUsers",
  components: {
    AdminNav
  },
  computed: {
    ...mapState(["currentUser"])
  },
  data() {
    return {
      users: {}
    };
  },
  methods: {
    async fetchUsers() {
      try {
        const { data, status, statusText } = await adminAPI.users.get();

        if (status !== 200) {
          throw new Error(statusText);
        }

        this.users = data.users;
      } catch (error) {
        console.error(error);

        Toast.fire({
          icon: "error",
          title: "無法取得使用者資料，請稍後嘗試"
        });
      }
    },
    async toggleUserRole(status, userId) {
      try {
        const isAdmin = status === "admin" ? "false" : "true";
        const { data } = await adminAPI.users.put({
          id: userId,
          isAdmin
        });

        if (data.status === "error") {
          throw new Error(data.message);
        }

        this.users = this.users.map(user => {
          // 如果使用者userId是要改選的對象，更換角色
          if (userId === user.id) {
            return {
              ...user,
              isAdmin: status === "admin" ? false : true
            };
          }
          return user;
        });
      } catch (error) {
        console.error(error);

        Toast.fire({
          icon: "error",
          title: "無法更新使用者角色，請稍後嘗試"
        });
      }
    }
  },
  created() {
    this.fetchUsers();
  }
};
</script>