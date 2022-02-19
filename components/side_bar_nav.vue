<template>
  <div>
    <div class="text-left sidebar-wrap" id="sidebar-wrapper">
      <div class="sidebar-heading text-center">
        <nuxt-link to="/" class="navbar-brand vank_logo_link"
          ><v-img src="/kyc.png" lazy-src="/male_avatar.png" alt="image"
        /></nuxt-link>
      </div>
      <div class="list-group list-group-flush my-3" id="menu_items">
        <nuxt-link
          to="/admin_dashboard/dashboard"
          class="list-group list-group-item active bg-transparent active"
        >
          <div class="child_items">
            <div class="ml-4 d-flex align-items-center">
              <v-img src="/home.png" lazy-src="/home.png" />
              <span class="ml-2 mt-1">Dashboard</span>
            </div>
          </div>
        </nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: false,
    };
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Space+Grotesk&family=Titillium+Web&display=swap");

* {
  margin: 0;
  padding: 0;
  font-family: "Space Grotesk", sans-serif;
  list-style-type: none !important;
  text-decoration: none !important;
}
.sidebar-wrap {
  background-color: #f8f7ff;
  /* background-color: #1d83c5 !important; */
}

#sidebar-wrapper {
  min-height: 100vh;
  /* margin-left: -14rem !important; */
  transition: margin 0.25s ease-out;
  position: fixed;
  z-index: 3;
}
#sidebar-wrapper .sidebar-heading {
  padding: 2.7rem 1.25rem !important;
  font-size: 1.2rem;
}
#sidebar-wrapper .list-group {
  width: 15rem;
}

#page-content-wrapper {
  min-width: 100vw;
}
#wrapper-toggled #sidebar-wrapper {
  margin-left: 0 !important;
}
#menu-toggle {
  cursor: pointer;
  /* display: none; */
}
.sidebar-heading .v-responsive {
  max-width: 150px;
}
.list-group-item {
  border: none;
  padding: 17px 30px !important;
  width: 100%;
  /* color: #c9cdcf !important; */
  color: #455b6d !important;
  cursor: pointer;
}
.list-group-item:hover {
  background-color: transparent !important;
  color: #455b6d !important;
  background-color: #ffffff !important;
  transition: all, 0.5s;
  border-radius: 0;
}
.img_wrap {
  width: 10%;
}
.child_items .v-responsive {
  max-width: 15px;
  height: 100%;
}

.list-group-item.active {
  border: none;
  background-color: transparent;
  color: #fff;
}
#wrapper .navbar {
  background-color: #fafafa;
  padding: 15px 10px !important;
  font-family: "Quicksand", sans-serif;
  text-decoration: none;
}
.status_toggle {
  cursor: pointer;
}
.custom-switch .custom-control-label::after {
  cursor: pointer;
}
.profile-wrapper,
.glee_history_wrapper {
  background-color: #fff;
  border-radius: 5px;
}
.purple_text {
  color: #55174f;
}
.line_height {
  line-height: 10px;
}
.creator_profile_pic {
  width: 100%;
  height: 13rem;
  border-radius: 20px;
  object-fit: cover;
  margin-top: 10px !important;
}
.child_wrapper {
  margin-left: 220px;
  overflow-y: hidden;
}

@media (max-width: 768px) {
  .sidebar-wrap {
    display: none;
  }
}
</style>