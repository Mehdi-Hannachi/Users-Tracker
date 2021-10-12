<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-logo-dark.png"
          transition="scale-transition"
          width="40"
        />

        <v-img
          alt="Vuetify Name"
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="100"
          src="https://cdn.vuetifyjs.com/images/logos/vuetify-name-dark.png"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
        <span class="mr-2">Latest Release</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-main>
      <UsersList
        @delete-user="deleteUser"
        :users="users"
        :updateUser="updateUser"
      />
      <UserModal @add-user="addUser" />
    </v-main>
  </v-app>
</template>


<script>
import UsersList from "./components/UsersList.vue";
import UserModal from "./components/UserModal.vue";
export default {
  name: "App",
  components: {
    UsersList,
    UserModal,
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
      this.users = data;
    },

    //Update user router
    async updateUser(id, updatedUser) {
      try {
        await fetch(`http://localhost:3000/users/${id}`, {
          method: "PUT",
          headers: {
            "Content-type": "application/json",
          },
          body: JSON.stringify(updatedUser),
        });
        // const data = await res.json();
        this.fetchUsers();
      } catch (error) {
        console.log("error put");
      }
    },
  },
  async created() {
    this.fetchUsers();
  },
};
</script>
