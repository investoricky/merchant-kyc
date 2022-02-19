<template>
  <nav class="user-side-bar">
    <div class="navbar sticky-top">
      <v-app-bar-nav-icon
        class="drawer"
        @click="drawer = true"
      ></v-app-bar-nav-icon>
      <v-spacer></v-spacer>
    </div>

    <v-navigation-drawer
      absolute
      temporary
      v-model="drawer"
      app
      class="primary"
    >
      <v-layout column align-center class="mt-5">
        <v-flex class="glee-wrap text-center">
          <nuxt-link to="/" class="navbar-brand vank_logo_link"></nuxt-link>
        </v-flex>
      </v-layout>
      <div class="list-group list-group-flush my-3" id="menu_items">
        <nuxt-link
          to="/user_dashboard/dashboard"
          class="list-group list-group-item active bg-transparent active"
        >
          <div class="child_items ml-5">
            <!-- <font-awesome-icon :icon="['fas', 'home']" /> -->
            <span class="ml-2">Dashboard</span>
          </div>
        </nuxt-link>
      </div>
    </v-navigation-drawer>
  </nav>
</template>

<script>
export default {
  data() {
    return {
      drawer: false,
    };
  },
  methods: {
    // async logout() {
    //   await this.$auth.logout();
    //   this.$router.push("/");
    //   this.$message({
    //     message: "You've Logged out!",
    //     type: "success",
    //   });
    // },
    // getuser() {
    //   this.$axios
    //     .get(this.baseUrl + "auth/user", {
    //       headers: {
    //         Authorization: `token ${localStorage.getItem("auth.jwt")}`,
    //       },
    //     })
    //     .then((response) => {
    //       console.log(response.data.data);
    //       this.profile = response.data.data.profile;
    //       this.wallet = response.data.data.wallet;
    //       console.log(this.wallet);
    //       // this.profile = response.data.data.profile;
    //       // console.log(response.data.data.profile.shoutout_price);
    //     });
    // },
  },
  mounted() {
    // this.getuser();
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk&family=Titillium+Web&display=swap");

* {
  margin: 0;
  padding: 0;
  font-family: "Space Grotesk", sans-serif;
  list-style-type: none !important;
  text-decoration: none !important;
}

#wrapper .navbar {
  background-color: transparent !important;
  padding: 15px 10px !important;
  font-family: "Quicksand", sans-serif;
  text-decoration: none;
}
.user-side-bar .v-overlay__scrim {
  min-height: 100vh;
}
.user-side-bar .v-navigation-drawer__content {
  background-color: #f8f7ff;
  text-decoration: none;
}
.user-side-bar .v-btn__content {
  display: none;
}
.user-side-bar .v-list-item__content {
  text-decoration: none !important;
}
.user-side-bar {
  display: none;
}
.user-side-bar .navbar {
  /* background-color: #fafafa; */
  padding: 5px 30px !important;
  font-family: "Quicksand", sans-serif;
  z-index: 1;
  text-decoration: none;
}
.user-side-bar .navbar-brand {
  color: #455b6d !important;

  font-size: 50px;
}
.user-side-bar ul {
  text-align: start;
  margin-top: 40px;
}
.list-group-flush > .list-group-item {
  border: none !important;
  color: #455b6d !important;
}
.user-side-bar .list {
  text-decoration: none;
  text-align: start;
  line-height: 55px;
  padding-left: 45px;
}

.user-side-bar .list:hover {
  color: #000;
}
.user-side-bar li:hover {
  background-color: #fdf3d9;
  color: #000 !important;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
}
.user-side-bar .admin {
  font-weight: 600;
}

@media (max-width: 768px) {
  .user-side-bar {
    display: block;
  }
  .user-side-bar .navbar {
    padding: 10px 0 !important;
  }
  .user-side-bar .bell {
    width: 85%;
  }
  .user-side-bar .v-btn__content {
    display: block;
  }
}
</style>