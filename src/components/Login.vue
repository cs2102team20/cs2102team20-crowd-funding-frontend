<script src="https://unpkg.com/axios/dist/axios.min.js"></script>
<template>
  <div>
    <b-container v-if="this.$store.state.auth.isLoggedIn">
      <h4>You are already logged in.</h4>
      <p>To log out, click on the button below.</p>
      <b-button variant="danger" @click="logout">Log Out</b-button>
    </b-container>
    <b-container v-else fluid>
      <b-row align-h="center">
        <b-col style=" max-width: 700px" align-self="center" xl="5" lg="6" md="7" sm="9">
          <b-form @submit="onSubmit" @reset="onReset">
            <b-form-group id="email-group" label="Email address:" label-for="email">
              <b-form-input
                id="email"
                v-model="form.email"
                type="email"
                required
                placeholder="Enter email"
              ></b-form-input>
            </b-form-group>

            <b-form-group id="password-group" label="Password:" label-for="password">
              <b-form-input
                id="password"
                v-model="form.password"
                type="password"
                required
                placeholder="Password"
              ></b-form-input>
            </b-form-group>

            <b-button style="margin: 2px" type="submit" variant="primary">Log In</b-button>
          </b-form>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      form: {
        email: "",
        password: ""
      }
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      this.$store
        .dispatch("login", {
          email: this.form.email,
          password_hash: this.form.password
        })
        .then(() => {
          this.$message("Login success.");
          this.$router.push("projects");
        })
        .catch((error) => {
          alert("Login failed." + error);
        });
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.password = "";
    },
    logout() {
      this.$store.dispatch("logout")
      .then(() => {
        this.$message("You've logged out!");
      })
    }
  }
};
</script>