<template>
  <div>
    <div class="update_kyc_details">
      <div class="px-3 mb-3" v-if="submitted">
        <div class="verified" >
          <div>
            <div class="icon-div">
              <ion-icon name="checkmark-outline"></ion-icon>
            </div>
            <h3 class="text-white">Update Succesful!</h3>
            <h3 >
              You can now Exit the browser</h3>
          </div>
        </div>
      </div>
      <div v-else>
        <h1 class="text-center text-white mt-4">Update KYC Details</h1>
        <div class="kyc_form_info">
          <div class="form_wrap p-3">
            <form action="" @submit.prevent="onSubmit()">
              <div class="">
                <p class="small mt-3" :class="[msg]">{{ msg }}</p>
                <div class="form-group mt-2">
                  <v-text-field
                    label="Ref Code"
                    v-model="kyc_info.reference_number"
                    placeholder="Enter Ref Code"
                    hint="Input Reference Code Sent To Your Mail"
                    required
                  />
                  <input type="button" class="check__kyc" @click="checkKYC" value="Confirm Reference">
                </div>
                <div v-if="other_details">
                  <div class="state_wrap">
                    <label for="">Select State</label>
                    <select
                      class="custom-select custom-select-sm"
                      id="selectState"
                      v-model="kyc_info.state"
                      @change="getState()"
                    >
                      <option value="---">---</option>
                      <option
                        v-for="item in states"
                        :key="item.id"
                        :value="item.name"
                        :id="item.alias"
                      >
                        {{ item.name }}
                      </option>
                    </select>
                  </div>

                  <div class="state_wrap mt-4">
                    <label for="">Select City</label>
                    <select
                      class="custom-select custom-select-sm"
                      v-model="kyc_info.city"
                    >
                      <option value="---">---</option>
                      <option
                        :value="item.name"
                        v-for="item in city"
                        :key="item.id"
                      >
                        {{ item.name }}
                      </option>
                    </select>
                  </div>

                  <div class="form-group mt-3">
                    <v-text-field
                      label="Valid Phone Number"
                      v-model="kyc_info.phone_number"
                      placeholder="Enter Phone Number"
                      required
                    />
                  </div>
                  
                  <div class="form-group mt-3">
                    <v-text-field
                      label="Address"
                      v-model="kyc_info.address"
                      placeholder="Enter Valid Business Address"
                      required
                    />
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
              </div>
            </form>
          </div>
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
      other_details: false,
      submitted: false,
      kyc_info: {
        reference_number: "",
        state: "",
        city: "",
        phone_number: "",
        address: '',
      },
      msg: "",
      states: [],
      city: [],
      selState: "",
    };
  },
  methods: {
    async checkKYC() {
      let payload = {
        reference_number: this.kyc_info.reference_number,
      };
      this.$axios
        .post("api/kyc/verify-reference", payload)
        .then((res) => {
          console.log(res);
          this.msg = res.data.message;
          if (res.data.message === "Reference Number is valid") {
            this.other_details = true;
          } else {
            this.other_details = false;
          }
          // this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          // this.loading = false;
        });
    },
    async onSubmit() {
      this.$axios
        .post("api/kyc/update", this.kyc_info)
        .then((res) => {
          // this.$router.push("/notification");
          this.kyc_info = {};
          console.log(res.data);
          // this.loading = false;
          this.submitted = true;
        })
        .catch((error) => {
          console.log(error);
          // this.loading = false;
        });
    },
    getState() {
      var stateOptions = document.getElementById("selectState");

      var selOption = stateOptions.options[stateOptions.selectedIndex].id;
      console.log(selOption);
      this.selState = selOption;
      this.getlgas();
    },
    async getStates() {
      let res = await this.$axios.get("https://locus.fkkas.com/api/states");
      this.states = res.data.data;
      console.log(this.states);
    },
    async getlgas() {
      let res = await this.$axios.get(
        `https://locus.fkkas.com/api/regions/${this.selState}`
      );
      this.city = res.data.data;
      console.log(this.city);
    },
  },
  async created() {
    this.getStates();
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
.check__kyc {
  background: #035303;
  color: #fff;
  padding: 0.2rem 1rem;
  font-size: 0.8rem;
  border-radius: 5px;
}
.valid {
  color: #035303;
}
.Invalid {
  color: #ff0000;
}
.verified {
  display: flex;
  /* width: 30%; */
  height: 100vh;
  align-items: center; 
  justify-content: center;
  /* position: absolute;
  top: 32%;
  left: 45%; */
  padding: 0.3rem 0.8rem;
  gap: 10px;
}
.verified ion-icon {
  color: #aff7af;
  font-weight: bold;
  font-size: 1.1rem;
  background-color: #aff7af3a;
  border: 1px solid #aff7af3a;
  border-radius: 50%;
  height: 8rem;
  width: 8rem;
}
.verified .icon-div {
  text-align: center;
  margin: 0 auto;
}
.verified h3{
  margin: 0;
  /* font-size: 0.8rem; */
  font-weight: bold;
  /* margin-top: -1.3rem; */
  color: #aff7af;
  text-align: center;
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