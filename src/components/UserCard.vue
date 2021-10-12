
<template>
  <v-card class="mx-auto" max-width="400">
    <v-img
      class="white--text align-end"
      height="200px"
      src="https://cdn.vuetifyjs.com/images/cards/docks.jpg"
    >
      <v-card-title> </v-card-title>
    </v-img>

    <v-card-subtitle class="pb-0">
      First Name : {{ user.firstName }}
    </v-card-subtitle>

    <v-card-text class="text--primary">
      <div>Last Name : {{ user.lastName }}</div>

      <div>Email : {{ user.email }}</div>
    </v-card-text>

    <v-card-actions class="btns">
      <v-btn color="red" text @click="deleteUser(user.id)"> Delete </v-btn>

      <UserModal :isUpdate="true" :user="user" :updateUser="updateUser" />
    </v-card-actions>
  </v-card>
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
