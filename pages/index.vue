<template>
  <div>
    <div class="kyc_wrap">
      <h1 class="text-center text-white">KYC Form</h1>
      <div class="kyc_form_info">
        <div class="span">
          <span
            ><b>IMPORTANT:</b> To ensure your KYC is aprroved, please upload the
            required documents in the appropriate fields.</span
          >
        </div>
        <div class="form_wrap mt-3">
          <form action="" @submit.prevent="onSubmit()">
            <div class="row">
              <div class="col-md-6">
                <div class="form-group mx-2 mt-4">
                  <v-text-field
                    label="Name"
                    v-model="kyc_info.name"
                    placeholder="Full Name"
                    required
                  />
                </div>
              </div>

              <div class="col-md-6">
                <div class="form-group mx-2 mt-4">
                  <v-text-field
                    label="E-mail"
                    v-model="kyc_info.email"
                    required
                  />
                </div>
              </div>
              <!-- Address -->
              <div class="col-md-6">
                <div class="form-group mx-2">
                  <v-text-field
                    label="Address"
                    v-model="kyc_info.address"
                    placeholder="Enter Address"
                    required
                  />
                </div>
              </div>
              <div class="col-md-6">
                <div class="form-group mx-2">
                  <v-text-field
                    type="number"
                    label="Phone Number"
                    v-model="kyc_info.phone_number"
                    required
                  />
                </div>
              </div>
              <!-- Country -->
              <div class="col-md-6">
                <div class="form-group mx-2">
                  <label for="exampleFormControlSelect1" class="py-2"
                    >State Of Origin</label
                  >
                  <select
                    class="form-control option-class select"
                    v-model="kyc_info.state"
                    @change="getState()"
                    id="selectState"
                  >
                    <option>---</option>
                    <option
                      v-for="state in states"
                      :key="state.id"
                      class="colour"
                      :value="state.alias"
                    >
                      {{ state.name }}
                    </option>
                  </select>
                </div>
              </div>
              <!-- City -->
              <div class="col-md-6">
                <div class="form-group mx-2">
                  <label for="exampleFormControlSelect1" class="py-2"
                    >L.G.A</label
                  >
                  <select
                    class="form-control option-class select"
                    id="exampleFormControlSelect1"
                    v-model="kyc_info.city"
                  >
                    <option>---</option>
                    <option
                      v-for="city of cities"
                      :key="city.id"
                      class="colour"
                      :value="city.name"
                    >
                      {{ city.name }}
                    </option>
                  </select>
                </div>
              </div>

              <div class="col-md-6">
                <div class="form-group">
                  <v-file-input
                    placeholder="Add your Passport"
                    prepend-icon="mdi-camera"
                    label="Passport Photo"
                    required
                    @change="upload_passport_photo()"
                  />
                </div>
              </div>
              <div class="col-md-6">
                <v-file-input
                  required
                  placeholder="Pick an Image of You and Your Shop"
                  prepend-icon="mdi-camera"
                  label="Image of You and Your Shop"
                  @change="upload_shop_photo()"
                />
              </div>
              <div class="col-md-6">
                <v-file-input
                  placeholder="Upload Relevant Business Document"
                  prepend-icon="mdi-camera"
                  label="Business Document(CAC or revenue receipt)"
                  @change="upload_relevant_doc()"
                />
              </div>
              <div class="col-md-12">
                <h5 class="text-center font-weight-bold">
                  VALID MEANS OF IDENTIFICATION
                </h5>
                <hr />
                <h6 class="py-3">
                  Government Issued Document
                  <i>(eg NIN, Voters Card, International Passport)</i>
                </h6>
                <div class="row mt-3">
                  <div class="col-md-12 py-3">
                    <v-file-input
                      required
                      placeholder="Pick a Valid Document"
                      prepend-icon="mdi-camera"
                      label="Valid Document"
                      @change="upload_valid_issued_id()"
                    />
                  </div>
                </div>
              </div>
              <div class="submit_button_wrapper">
                <v-btn type="submit" :loading="loading">Submit</v-btn>
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
  name: "IndexPage",
  data() {
    return {
      loading: false,
      kyc_info: {
        name: "",
        email: "",
        address: "",
        reference_number: "",
        passport_photo: "",
        shop_photo: "",
        valid_id: "",
        relevant_document: "",
        phone_number: "",
        state: "",
        city: "",
      },
      document: [],
      states: {},
      selState: "",
      cities: "",
      stateUrl: "https://locus.fkkas.com/api/states",
    };
  },
  methods: {
    getState() {
      var stateOptions = document.getElementById("selectState");
      var selOption = stateOptions.options[stateOptions.selectedIndex].value;
      this.selState = selOption;
      this.get_cities();
    },
    get_kyc() {
      this.loading = true;
      const formData = new FormData();
      formData.append("name", this.kyc_info.name);
      formData.append("email", this.kyc_info.email);
      formData.append("phone_number", this.kyc_info.phone_number);
      formData.append("passport_photo", this.kyc_info.passport_photo);
      formData.append("shop_photo", this.kyc_info.shop_photo);
      formData.append("valid_id", this.kyc_info.valid_id);
      formData.append("state", this.kyc_info.state);
      formData.append("city", this.kyc_info.city);
      formData.append("address", this.kyc_info.address);
      formData.append("relevant_document", this.kyc_info.relevant_document);
      formData.append("_method", "POST");
      this.$axios
        .post("/api/kyc/create", formData)
        .then((res) => {
          this.$router.push("/notification");
          this.kyc_info = {};
          // console.log(res.data);
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },

    async get_states() {
      try {
        const response = await this.$axios.get(this.stateUrl);
        this.states = response.data.data;
        console.log(this.states);
      } catch (error) {
        console.log(error.response);
      }
    },
    async get_cities() {
      let res = await this.$axios.get(
        `https://locus.fkkas.com/api/regions/${this.selState}`
      );
      this.cities = res.data.data;
    },
    upload_passport_photo() {
      var input = event.target;
      this.kyc_info.passport_photo = input.files[0];
      this.document.push(this.kyc_info.passport_photo);
      // console.log(this.kyc_info.passport_photo);
    },
    upload_shop_photo() {
      var input = event.target;
      this.kyc_info.shop_photo = input.files[0];
      this.document.push(this.kyc_info.shop_photo);
      // console.log(this.kyc_info.shop_photo);
    },
    upload_relevant_doc() {
      var input = event.target;
      this.kyc_info.relevant_document = input.files[0];
      // console.log(this.kyc_info.relevant_document);
      this.document.push(this.kyc_info.relevant_document);
    },

    upload_valid_issued_id() {
      var input = event.target;
      this.kyc_info.valid_id = input.files[0];
      this.document.push(this.kyc_info.valid_id);
      // console.log(this.kyc_info.valid_id);
    },
    onSubmit() {
      this.get_kyc();
    },
  },
  mounted() {
    this.get_states();
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
}
.kyc_wrap {
  background: url("https://www.athletadesk.com/wp-content/uploads/2016/08/join-background.jpg");
  background-color: rgba(0, 0, 0, 0.7);
  background-blend-mode: overlay;
  padding: 2rem;
}
.kyc_form_info input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
.kyc_wrap h1 {
  font-size: 1.5rem;
  font-weight: bold;
}
.kyc_form_info {
  /* background-color: rgba(240, 248, 255, 0.3); */
  background: #fff;
  width: 50%;
  margin: 0 auto;
  border-radius: 10px;
  padding: 10px 30px;
  box-shadow: 0px 0px 5px 1px rgba(0, 0, 0, 0.125);
}
.kyc_form_info h1 {
  text-align: center;
  font-size: 30px;
  margin-top: 20px;
}
.kyc_form_info .span span {
  font-size: 12px;
  color: #f00;
}
.kyc_form_info .form-control {
  height: 50px;
}
.submit_button_wrapper {
  width: 100%;
  padding: 20px;
}
.kyc_form_info .option-class {
  box-shadow: none;
}
.kyc_form_info .option-class:focus-within {
  border-color: #30303025;
}
.submit_button_wrapper .v-btn {
  width: 100%;
  height: 40px;
  box-shadow: none;
  background-color: green !important;
  color: #fff !important;
}
.v-file-input label,
.v-text-field label {
  font-size: 13px;
}

@media (max-width: 768px) {
  .kyc_wrap {
    padding: 10px;
  }
  .kyc_form_info {
    width: 100%;
    margin: 0;
    padding: 20px;
  }
  .kyc_form_info .form-group {
    font-size: 14px;
  }
  .kyc_form_info .col-md-6 {
    padding: 5px !important;
  }
  .kyc_form_info .mt-4 {
    margin-top: 0 !important;
  }
  .kyc_form_info h6 {
    font-size: 13px;
  }
}
</style>
