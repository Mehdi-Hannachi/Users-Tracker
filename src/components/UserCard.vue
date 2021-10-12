<template>
  <div>
    <h1>User Card</h1>
    <div>
      <h3>{{ user.firstName }}</h3>
      <h3>{{ user.lastName }}</h3>
      <h3>{{ user.email }}</h3>
      <button @click="deleteUser(user.id)">x</button>

      <UserModal :isUpdate="true" :user="user" :updateUser="updateUser" />
    </div>
  </div>
</template>

<script>
import UserModal from "./UserModal.vue";

export default {
  name: "UserCard",

  components: {
    UserModal,
  },
  props: {
    user: Object,
    updateUser: Function,
  },
  methods: {
    deleteUser(id) {
      this.$emit("delete-user", id);
    },
  },
};
</script>
