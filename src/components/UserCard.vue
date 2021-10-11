<template>
  <div>
    <h1>User Card</h1>
    <div>
      <h3>{{ user.firstName }}</h3>
      <h3>{{ user.lastName }}</h3>
      <h3>{{ user.email }}</h3>
      <button @click="deleteUser(user.id)">x</button>
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
    deleteUser(id) {
      this.$emit('delete-user',id)
    },
  },
};
</script>
