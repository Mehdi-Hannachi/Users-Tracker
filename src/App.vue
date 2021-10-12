<template>
  <div>
    <UsersList @delete-user="deleteUser" :users="users" />
    <AddUser @add-user="addUser" />
  </div>
</template>

<script>
import UsersList from "./components/UsersList.vue";
import AddUser from "./components/AddUser.vue";

export default {
  name: "App",
  components: {
    UsersList,
    AddUser,
  },

  data() {
    return {
      users: [],
    };
  },

  methods: {
    // Adding a user route

    async addUser(user) {
      const res = await fetch(`http://localhost:3000/users`, {
        method: `POST`,
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(user),
      });

      const data = await res.json();

      this.users = [...this.users, data];
    },

    // Deleting user route

    async deleteUser(id) {
      if (confirm(`Are you sure you want to delete this user ? `)) {
        const res = await fetch(`http://localhost:3000/users/${id}`, {
          method: `DELETE`,
        });

        res.status === 200
          ? (this.users = this.users.filter((user) => user.id !== id))
          : alert(`  User deleting failed`);
      }
    },

    // Get all users route

    async fetchUsers() {
      const res = await fetch(`http://localhost:3000/users`);
      // console.log(res);
      const data = await res.json();
      // console.log(data);
      return data;
    },
  },

  async created() {
    this.users = await this.fetchUsers();
  },
};
</script>

