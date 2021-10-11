<template>
  <div>
    <h1>User Card</h1>
    <div>
      <h3>{{ user.firstName }}</h3>
      <h3>{{ user.lastName }}</h3>
      <h3>{{ user.email }}</h3>
      <button @click="deleteUser(user.id)">x</button>
      <button @click="editUser(user.id, user)">Edit</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "UserCard",
  props: {
    user: Object,
  },
  methods: {
    editUser(id, user) {
      this.$emit("edit-user", id, user);
    },
    deleteUser(id) {
      this.$emit("delete-user", id);
    },
  },
};
</script>
