<template>
  <form @submit="onSubmit">
    <label> First Name : </label>
    <input v-model="firstName" type="text" />
    <label> Last Name : </label>
    <input v-model="lastName" type="text" />
    <label> Email : </label>
    <input v-model="email" type="Email" />
    <button>Add user</button>
  </form>
</template>

<script>
export default {
  name: "AddUser",
  data() {
    return {
      firstName: "",
      lastName: "",
      email: "",
    };
  },

  methods: {
    onSubmit(e) {
      e.preventDefault();
      if (!this.firstName) {
        alert("Please enter your first name");
        return;
      }
      if (!this.lastName) {
        alert("Please enter your last name");
        return;
      }
      if (!this.email) {
        alert("Please enter your email");
        return;
      }
      const newUser = {
        id: Math.floor(Math.random() * 100000),
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
      };
      this.$emit("add-user", newUser);
      alert("User added with success");
      this.firstName = "";
      this.lastName = "";
      this.email = "";
    },
  },
};
</script>