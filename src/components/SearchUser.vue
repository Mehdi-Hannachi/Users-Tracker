<template>
  <div>
    <v-text-field
      label="Search by First Name"
      placeholder="Search ..."
      @input="searchByName"
      outlined
    ></v-text-field>
    <v-text-field
      label="Search by Last Name"
      @input="searchByLastName"
      placeholder="Search ..."
      outlined
    ></v-text-field>
    <v-text-field
      label="Search by Email"
      @input="searchByEmail"
      placeholder="Search ..."
      outlined
    ></v-text-field>
  </div>
</template>

<script>
export default {
  name: "SearchUser",

  methods: {
    searchByName(e) {
      this.$emit("handelFirstName", e);
    },
    searchByLastName(e) {
      this.$emit("handelLastName", e);
    },
    searchByEmail(e) {
      this.$emit("handelEmail", e);
    },
  },
};
</script>
