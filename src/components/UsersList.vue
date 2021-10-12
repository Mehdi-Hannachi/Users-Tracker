<template>
  <div>
    <h1>Users List</h1>
    <div :key="user.id" v-for="user in users">
      <UserCard
        @delete-user="$emit('delete-user', user.id)"
        :updateUser="updateUser"
        :user="user"
      />
    </div>
  </div>
</template>

<script>
import UserCard from "./UserCard.vue";
export default {
  name: "UsersList",
  props: {
    users: Array,
    updateUser: Function,
  },

  components: {
    UserCard,
  },
  emits: ["delete-user"],

  async created(){
      this.users.filter((user) =>
        user.firstName
          .toLowerCase()
          .includes(this.firstNameTextSeacrh.toLowerCase())
      );
  }
};
</script>