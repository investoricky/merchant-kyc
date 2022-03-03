<template>
  <div>
    <div class="update_kyc_details">
      <h1 class="text-center text-white">KYC Form</h1>
      <div class="kyc_form_info">
        <div class="form_wrap mt-3">
          <form action="" @submit.prevent="onSubmit()">
            <div class="">
              <div class="form-group mx-2 mt-2">
                <v-text-field
                  label="Ref Code"
                  v-model="kyc_info.reference_number"
                  placeholder="Enter Ref Code"
                  hint="Input Reference Code Sent To Your Mail"
                  required
                />
              </div>
              <div class="state_wrap">
                <select class="custom-select custom-select-sm">
                  <option selected>Open this select menu</option>
                  <option value="1">One</option>
                  <option value="2">Two</option>
                  <option value="3">Three</option>
                </select>
              </div>

              <div class="state_wrap mt-4">
                <select class="custom-select custom-select-sm">
                  <option selected>Open this select menu</option>
                  <option value="1">One</option>
                  <option value="2">Two</option>
                  <option value="3">Three</option>
                </select>
              </div>

              <div class="submit_button_wrapper mt-4">
                <v-btn
                  class="success bg-success apply-to-join-btn"
                  type="submit"
                  :loading="loading"
                  >Submit</v-btn
                >
              </div>
            </div>
          </form>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      loading: false,
      kyc_info: {
        reference_number: "",
        state: "",
        city: "",
      },

      state: {},
      city: {},
    };
  },
};
</script>

<style>
.update_kyc_details {
  background: url("https://www.athletadesk.com/wp-content/uploads/2016/08/join-background.jpg");
  background-color: rgba(0, 0, 0, 0.7);
  background-blend-mode: overlay;
  padding: 2rem;
  min-height: 100vh;
}
.update_kyc_details .kyc_form_info {
  /* background-color: rgba(240, 248, 255, 0.3); */
  background: #fff;
  width: 50%;
  margin: 0 auto;
  border-radius: 10px;
  padding: 50px 30px;
  box-shadow: 0px 0px 5px 1px rgba(0, 0, 0, 0.125);
}
.update_kyc_details .submit_button_wrapper {
  width: 100%;
}
.update_kyc_details .submit_button_wrapper .v-btn {
  width: 100%;
  height: 30px;
  box-shadow: none;
  text-transform: none;
}
.update_kyc_details .v-file-input label,
.update_kyc_details .v-text-field label {
  font-size: 13px;
}
.update_kyc_details .state_wrap .custom-select {
  box-shadow: none;
}
.update_kyc_details .state_wrap .custom-select:focus-within {
  border-color: #30303025;
}

@media (max-width: 768px) {
  .update_kyc_details {
    padding: 1rem;
  }
  .update_kyc_details .kyc_form_info {
    width: 100%;
    margin: 0;
    padding: 10px;
  }
}
</style>