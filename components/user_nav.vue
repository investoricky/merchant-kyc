<template>
  <div>
    <div class="nav_content w-100">
      <nav
        class="navbar navbar-expand-lg navbar-light bg-transparent py-4 px-1"
      >
        <div class="">
          <li class="dashboard_text_li d-flex align-items-center">
            <div><creator-sidebar /></div>
            <h1 class="dashboard_text blue_text mt-3">{{ name }}</h1>
          </li>
        </div>
        <v-spacer></v-spacer>
        <div class="d-flex align-items-center">
          <div class="mx-2">
            <!-- <font-awesome-icon :icon="['fas', 'bell']" /> -->
          </div>
          <div class="mx-2">
            <button @click="logout()" class="log_out_button">Logout</button>
          </div>
        </div>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  props: ["name"],
  methods: {
    async logout() {
      await this.$auth.logout();
      this.$router.push("/");
      this.$toast.success("You've Successfully Logged Out", {
        timeout: 5000,
      });
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk&family=Titillium+Web&display=swap");

* {
  margin: 0;
  padding: 0;
  font-family: "Space Grotesk", sans-serif;
}
.log_out_button {
  border: 1px solid #00e8fe;
  padding: 5px 15px;
  border-radius: 5px;
}
@media (max-width: 768px) {
  .dashboard_text {
    font-size: 20px;
    margin-top: 0 !important;
  }
  .navbar {
    padding: 0 !important;
  }
}
</style>