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
    addUser(user) {
      this.users = [...this.users, user];
    },

    deleteUser(id) {
      this.users = this.users.filter((user) => user.id !== id);
    },
  },

  created() {
    this.users = [
      {
        id: 1,
        firstName: "Mehdi",
        lastName: "Hannachi",
        email: "mehdihannachi02@gmail.com",
      },
      {
        id: 2,
        firstName: "Mohamed",
        lastName: "Hannachi",
        email: "mohamedhannachi02@gmail.com",
      },
      {
        id: 3,
        firstName: "mariem",
        lastName: "Hannachi",
        email: "mariemhannachi02@gmail.com",
      },
    ];
  },
};
</script>

<style>
</style>
