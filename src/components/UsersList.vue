<template>
  <div class="d-flex justify-space-around flex-wrap ma-4">
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
};
</script>