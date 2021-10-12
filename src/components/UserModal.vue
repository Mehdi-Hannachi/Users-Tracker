
<template>
  <v-row justify="center">
    <v-dialog v-model="dialog" persistent max-width="600px">
      <template v-slot:activator="{ on, attrs }">
        <v-btn color="primary" dark v-bind="attrs" v-on="on"
          >{{ isUpdate ? "Update" : "Add" }} User
        </v-btn>
      </template>
      <v-card>
        <v-card-title>
          <span class="text-h5">{{ isUpdate ? "Update" : "Add" }} User</span>
        </v-card-title>
        <v-card-text>
          <v-container>
            <v-row>
              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Legal first name*"
                  v-model="firstName"
                  required
                ></v-text-field>
              </v-col>

              <v-col cols="12" sm="6" md="4">
                <v-text-field
                  label="Legal last name*"
                  v-model="lastName"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12">
                <v-text-field
                  label="Email*"
                  v-model="email"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
          <small>*indicates required field</small>
        </v-card-text>
        <v-card-actions>
          <v-spacer></v-spacer>
          <v-btn color="blue darken-1" text @click="dialog = false">
            Close
          </v-btn>
          <v-btn color="blue darken-1" text @click="updateAddUser"> Save </v-btn>
        </v-card-actions>
      </v-card>
    </v-dialog>
  </v-row>
</template>

<script>
export default {
  name: "UserModal",
  data() {
    return {
      firstName: this.isUpdate ? this.user.firstName : "",
      lastName: this.isUpdate ? this.user.lastName : "",
      email: this.isUpdate ? this.user.email : "",
      dialog: false,
    };
  },

  props: ["isUpdate", "updateUser", "user"],

  methods: {
    emptiedfields() {
      this.firstName = "";
      this.lastName = "";
      this.email = "";
    },

    closeModal() {
      this.dialog = false;
    },

    addUser() {
      
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
        // id: Math.floor(Math.random()),
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
      };
      this.$emit("add-user", newUser);
      this.emptiedfields();
      this.closeModal();
    },

    update() {
      this.updateUser(this.user.id, {
        firstName: this.firstName,
        lastName: this.lastName,
        email: this.email,
      });
      this.emptiedfields();
      this.closeModal();
    },

    updateAddUser() {
      this.isUpdate ? this.update() : this.addUser();
    },
  },
};
</script>