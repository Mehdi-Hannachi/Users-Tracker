<template>
  <v-row justify="center" class="mt-8 mx-5">
    <v-col>
      <v-text-field
        label="Search by First Name"
        placeholder="Search ..."
        @input="searchByName"
        outlined
      ></v-text-field>
    </v-col>
    <v-col>
      <v-text-field
        label="Search by Last Name"
        @input="searchByLastName"
        placeholder="Search ..."
        outlined
      ></v-text-field>
    </v-col>
    <v-col>
      <v-text-field
        label="Search by Email"
        @input="searchByEmail"
        placeholder="Search ..."
        outlined
      ></v-text-field>
    </v-col>
  </v-row>
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
