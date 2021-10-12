<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <v-img
          alt="Vuetify Logo"
          class="shrink mr-2"
          contain
          src="https://www.shareicon.net/data/2015/07/04/64248_users_256x256.png"
          transition="scale-transition"
          width="90"
        />

        <v-img
          class="shrink mt-1 hidden-sm-and-down"
          contain
          min-width="150"
          width="100"
        />
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/vuetifyjs/vuetify/releases/latest"
        target="_blank"
        text
      >
      </v-btn>
    </v-app-bar>

    <v-main>
      <SearchUser
        v-on:handelFirstName="handelFirstName"
        v-on:handelLastName="handelLastName"
        v-on:handelEmail="handelEmail"
      />
      <UsersList
        @delete-user="deleteUser"
        :users="filterUsers(users)"
        :updateUser="updateUser"
        :firstNameTextSeacrh="firstNameTextSeacrh"
      />
    </v-main>
    <UserModal @add-user="addUser" />
  </v-app>
</template>


<script>
import UsersList from "./components/UsersList.vue";
import UserModal from "./components/UserModal.vue";
import SearchUser from "./components/SearchUser.vue";
export default {
  name: "App",
  components: {
    UsersList,
    UserModal,
    SearchUser,
  },
  data() {
    return {
      users: [],
      firstNameTextSeacrh: "",
      lastNameTextSearch: "",
      emailTextSearch: "",
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

    //Update user route
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

    // Get search inputs values
    handelFirstName(txt) {
      this.firstNameTextSeacrh = txt.toLowerCase();
    },
    handelLastName(txt) {
      this.lastNameTextSearch = txt.toLowerCase();
    },
    handelEmail(txt) {
      this.emailTextSearch = txt.toLowerCase();
    },

    //Filter users
    filterUsers(usersList) {
      return usersList.filter(({ firstName, lastName, email }) => {
        return (
          firstName.toLowerCase().includes(this.firstNameTextSeacrh) &&
          lastName.toLowerCase().includes(this.lastNameTextSearch) &&
          email.toLowerCase().includes(this.emailTextSearch)
        );
      });
    },
  },
  async created() {
    this.fetchUsers();
  },
};
</script>
