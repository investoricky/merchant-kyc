<template>
  <div class="admin_login_wrap">
    <div class="login-content">
      <div class="login_section">
        <form class="mt-3" method="post" @submit.prevent="onSubmit()">
          <div class="form-group py-3">
            <label class="py-2" for="">Email</label>
            <input
              type="text"
              class="form-control"
              v-model="credentials.email"
              placeholder="Enter your Email Address"
            />
          </div>
          <div class="form-group py-3">
            <label class="py-2" for="">Password</label>
            <div
              class="
                d-flex
                password_wrap
                align-items-center
                justify-content-between
              "
            >
              <input
                type="password"
                id="password"
                class=""
                v-model="credentials.password"
                required
                placeholder="Enter Password"
              />
              <span class="d-flex" @click="displayPassword()">
                <!-- <font-awesome-icon
                  id="show_password"
                  class="text-muted eye_icon"
                  :icon="['fas', 'eye']"
                /> -->
                <!-- <font-awesome-icon
                  id="hide_password"
                  class="text-muted eye_slash_icon"
                  :icon="['fas', 'eye-slash']"
                /> -->
              </span>
            </div>
            <div class="text-right">
              <nuxt-link to="/forgot_password" class="password_link"
                >forgot password?</nuxt-link
              >
            </div>
          </div>

          <div class="text-center">
            <v-btn
              class="login_button"
              :loading="loading"
              value="Login"
              type="submit"
              >Log In</v-btn
            >
            <div class="login_wrap mt-3">
              <p>
                Don’t have an account?
                <nuxt-link
                  to="/sign_up"
                  class="sign_up_link text-decoration-none"
                  >Sign up here</nuxt-link
                >
              </p>
            </div>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  components: {},
  data() {
    return {
      credentials: {
        email: "",
        password: "",
      },
      loading: false,
    };
  },

  methods: {
    // async userLogin() {
    //   try {
    //     // this.isLoading = true;
    //     let response = await this.$auth.loginWith("local", {
    //       data: this.login,
    //     });
    //     console.log(response);
    //     if (response.status == 200) {
    //       // this.isLoading = false;
    //       console.log(response.data.token);
    //       this.$auth.setUserToken(response.data.token);
    //       // this.$auth.setUser(response.data.data.user);
    //       this.$router.push("/admin_dashboard/dashboard");
    //       console.log(this.$auth.loggedIn);
    //       this.$toast.success("Welcome", {
    //         timeout: 5000,
    //       });
    //       //  this.$toast.success('Successfully authenticated');
    //     } else {
    //       // this.isLoading = false;
    //       console.log(response.user.message);
    //       this.$toast.warning("Please Try Again", {
    //         timeout: 5000,
    //       });
    //     }
    //   } catch (err) {
    //     this.isLoading = false;
    //     console.log(err.response);
    //     // this.$toast.warning(err.response.data.data, {
    //     //   timeout: 5000,
    //     // });
    //   }
    // },
    async userLogin() {
      try {
        this.loading = true;
        let response = await this.$auth.loginWith("local", {
          data: this.credentials,
        });
        console.log(response);
        this.$auth.setUserToken(response.data.token);
        this.$router.push("/admin_dashboard/dashboard");
        this.$toast.success("Welcome", {
          timeout: 5000,
        });
      } catch (err) {
        this.loading = false;
        this.$toast.warning(
          "There was a problem logging into your account. Please try again.",
          {
            timeout: 5000,
          }
        );
        console.log(err);
      }
    },

    displayPassword() {
      let password = document.getElementById("password");
      let show_password = document.getElementById("show_password");
      let hide_password = document.getElementById("hide_password");
      if (password.type === "password") {
        password.type = "text";
        show_password.style.display = "block";
        hide_password.style.display = "none";
      } else {
        password.type = "password";
        show_password.style.display = "none";
        hide_password.style.display = "block";
      }
    },
    onSubmit() {
      this.userLogin();
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Titillium+Web&display=swap");
* {
  margin: 0;
  padding: 0;
  font-family: "Space Grotesk", sans-serif;
  text-decoration: none !important;
}
.v-btn {
  background-color: #00e8fe !important;
  color: #000 !important;
  text-transform: none;
  padding: 25px 30px !important;
  width: 30%;
  font-size: 18px;
  width: 100%;
  box-shadow: none;
}

.eye_icon {
  font-size: 15px;
  display: none;
  cursor: pointer;
}
.eye_slash_icon {
  font-size: 15px;
  cursor: pointer;
}

.form-control {
  color: grey;
  min-height: 7vh;
  padding: 10px;
}

.password_wrap {
  border-radius: 0.25rem;
  display: block;
  width: 100%;
  padding: 10px;
  height: calc(2em + 0.75rem + 2px);
  font-size: 1rem;
  font-weight: 400;
  color: #495057;
  border: 1px solid #ced4da !important;
  background-clip: padding-box;
  border: 1px solid #ced4da;
  border-radius: 0.35rem;
}
.password_wrap input {
  width: 100%;
  outline: none;
  color: grey;
}

.form-control:focus {
  box-shadow: none;
  border-color: #c5cbcc;
}
.forgot-password-wrap {
  cursor: pointer;
}
.password_link,
.sign_up_link {
  cursor: pointer;
  color: #1d83c5;
  font-size: 13px;
}
.login_wrap {
  font-size: 14px;
}

@media (max-width: 768px) {
  .password_wrap {
    font-size: 13px;
  }
  .form-control,
  label,
  .login_wrap,
  .password_link,
  .sign_up_link {
    font-size: 13px;
  }
  .login_button {
    font-size: 15px;
  }
  .form-control {
    height: 5%;
  }
}
</style>