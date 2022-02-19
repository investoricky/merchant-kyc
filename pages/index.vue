<template>
  <div>
    <div class="kyc_wrap">
      
        <h1 class="text-center text-white">KYC Form</h1>
      <div class="kyc_form_info">
        <div class="form_wrap mt-3">
          <form action="" @submit.prevent="onSubmit()">
            <div class="row">
              <div class="col-md-6">
                <div class="form-group mx-2 mt-2 py-3">
                  <v-text-field
                    label="Name"
                    v-model="kyc_info.name"
                    placeholder="Full Name"
                    required
                  />
                </div>
              </div>

              <div class="col-md-6">
                <div class="form-group mx-2 mt-2 py-3">
                  <v-text-field
                    label="E-mail"
                    v-model="kyc_info.email"
                    required
                  />
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
              <!-- <div class="col-md-6">
                <v-file-input
                  multiple
                  placeholder="Upload Relevant Business Document"
                  prepend-icon="mdi-camera"
                  label="Business Document(Revenue Receipt)"
                  @change="upload_revenue_receipt()"
                />
              </div> -->
              <div class="col-md-12">
                <h5 class="text-center font-weight-bold">VALID MEANS OF IDENTIFICATION</h5>
                <hr>
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
  name: "IndexPage",
  data() {
    return {
      loading: false,
      kyc_info: {
        name: "",
        email: "",
        reference_number: "",
        passport_photo: "",
        shop_photo: "",
        valid_id: "",
        relevant_document: "",
      },
      document: [],
    };
  },
  methods: {
    // async get_kyc() {
    //   try {
    //     this.loading = true;
    //     let payload = {
    //       name: this.kyc_info.name,
    //       email: this.kyc_info.email,
    //       // reference_number = this.kyc_info.reference_number,
    //       // passport_photo: this.kyc_info.passport_photo,
    //       // valid_id: this.kyc_info.valid_id,
    //       // relevant_document: this.kyc_info.relevant_document,
    //       // shop_photo: this.kyc_info.shop_photo,
    //       documents: this.document,
    //     };
    //     const response = await this.$axios.post("/api/kyc/create", payload);
    //     // console.log(this.kyc_info);

    //     console.log(response);
    //     this.loading = false;
    //     this.$router.push("/notification");
    //   } catch (error) {
    //     console.log(error.response);
    //     this.loading = false;
    //   }
    // },
    get_kyc() {
      this.loading = true;
      const formData = new FormData();
      formData.append("name", this.kyc_info.name);
      formData.append("email", this.kyc_info.email);
      formData.append("passport_photo", this.kyc_info.passport_photo);
      formData.append("shop_photo", this.kyc_info.shop_photo);
      formData.append("valid_id", this.kyc_info.valid_id);
      formData.append("relevant_document", this.kyc_info.relevant_document);
      formData.append("_method", "POST");
      this.$axios
        .post("/api/kyc/create", formData)
        .then((res) => {
          this.$router.push("/notification");
          this.kyc_info = {};
          console.log(res.data);
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
    },
    upload_passport_photo() {
      var input = event.target;
      this.kyc_info.passport_photo = input.files[0];
      this.document.push(this.kyc_info.passport_photo);
      console.log(this.kyc_info.passport_photo);
    },
    upload_shop_photo() {
      var input = event.target;
      this.kyc_info.shop_photo = input.files[0];
      this.document.push(this.kyc_info.shop_photo);
      console.log(this.kyc_info.shop_photo);
    },
    upload_relevant_doc() {
      var input = event.target;
      this.kyc_info.relevant_document = input.files[0];
      console.log(this.kyc_info.relevant_document);
      this.document.push(this.kyc_info.relevant_document);
    },

    upload_valid_issued_id() {
      var input = event.target;
      this.kyc_info.valid_id = input.files[0];
      this.document.push(this.kyc_info.valid_id);
      console.log(this.kyc_info.valid_id);
    },
    onSubmit() {
      this.get_kyc();
    },
  },
};
</script>


<style>
* {
  margin: 0;
  padding: 0;
}
.kyc_wrap {
  background: url('https://www.athletadesk.com/wp-content/uploads/2016/08/join-background.jpg');
  background-color: rgba(0, 0, 0, 0.7);
  background-blend-mode: overlay;
   padding: 2rem;
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
/* .kyc_form_info span {
  font-size: 10px !important;
} */
.kyc_form_info .form-control {
  height: 50px;
}
.submit_button_wrapper {
  width: 100%;
  padding: 20px;
}
.submit_button_wrapper .v-btn {
  width: 100%;
  height: 40px;
  box-shadow: none;
}
.v-file-input label,
.v-text-field label {
  font-size: 13px;
}

@media (max-width: 768px) {
  .kyc_form_info {
    width: 100%;
    margin: 0;
    padding: 20px;
  }
}
</style>
