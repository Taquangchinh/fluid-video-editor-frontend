<template>
  <v-container fluid fill-height class="bg-img">
    <v-row align="center" justify="end">
      <v-col cols="12" sm="4" md="4">
        <v-card @keydown.enter="login" class="elevation-2" max-width="50vh">
          <v-toolbar color="#517EA9" dark flat>
            <v-toolbar-title>Login</v-toolbar-title>
            <v-spacer />
            <v-icon>fa fa-user</v-icon>
          </v-toolbar>
          <v-card-text>
            <v-alert v-if="error" type="error">
              {{ error }}
            </v-alert>
            <v-form>
              <v-select
                prepend-icon="fa fa-user-tag"
                :items="roles"
                label="Role"
                v-model="role"
              ></v-select>
              <v-text-field
                label="User Name"
                autofocus
                @focus="error = null"
                prepend-icon="fa fa-user"
                type="text"
                v-model="username"
              />

              <v-text-field
                label="Password"
                @focus="error = null"
                prepend-icon="fa fa-lock"
                type="password"
                v-model="password"
              />
            </v-form>
          </v-card-text>
          <v-card-actions>
            <v-spacer />
            <v-btn block color="#F1C42E" @click="login">Login</v-btn>
          </v-card-actions>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";
import { mapMutations } from "vuex";
export default {
  data() {
    return {
      username: null,
      password: null,
      role: "Admin",
      error: null,
      roles: ["Admin", "User"]
    };
  },
  methods: {
    ...mapMutations(["setToken", "setUser", "setProfile"]),
    async login() {
      let username = this.username;
      let password = this.password;
      if (this.role == "Admin") {
        try {
          let result = await axios.post(this.API_URL + "/api/admin/login", {
            username,
            password
          });
          let token = result.data.token;
          let profileObj = {
            name: result.data.name,
            avatar: result.data.avatar,
            group: result.data.group
          };
          this.setToken(token);
          this.setUser({
            is_logged: true,
            role: "admin"
          });
          this.setProfile(profileObj);
          this.$router.push("/");
        } catch (error) {
          this.error = "Invalid Username/Password";
        }
      }

      if (this.role == "User") {
        try {
          let result = await axios.post(this.API_URL + "/api/user/login", {
            username,
            password
          });
          let token = result.data.token;
          let user_id = result.data.user_id;
          let profileObj = {
            name: result.data.name,
            avatar: result.data.avatar,
            group: result.data.group
          };
          this.setToken(token);
          this.setUser({
            is_logged: true,
            role: "user"
          });
          this.setProfile(profileObj);
          this.$router.push("/user/" + user_id);
        } catch (error) {
          this.error = "Invalid Username/Password";
        }
      }
    }
  }
};
</script>

<style scoped>
.bg-img {
  background-image: url("/login.png");
  background-position: left;
  background-repeat: no-repeat;
  background-size: contain;
  position: relative;
}
</style>
