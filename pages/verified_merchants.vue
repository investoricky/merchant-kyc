<template>
  <div>
    <div class="verified_merchant_wrap">
      <div class="verification_content">
        <div
          class="
            form-group
            w-50
            search-area
            mx-auto
            d-flex
            align-items-center
            mt-3
          "
        >
          <v-text-field
            label="Search"
            v-model="search"
            placeholder="Search Merchant by City"
            required
            @keyup="getKYC(search)"
          />
          <button class="btn__search" @click="getKYC(search)">
            <ion-icon name="search"></ion-icon>
          </button>
        </div>
        <div class="text-center py-3">
          <h1 class="font-weight-bold">SZC Verified Merchants</h1>
          <hr style="width: 20%; margin: 0 auto" />
        </div>
        <div class="table-responsive">
          <v-simple-table fixed-header height="500px">
            <template v-slot:default>
              <thead>
                <tr class="">
                  <td class="text-left th_color"></td>
                  <th class="text-left th_color">Reference No</th>
                  <th class="text-left th_color">Name</th>
                  <!-- <th class="text-left th_color">Email</th> -->
                  <th class="text-left th_color">Phone No</th>
                  <th class="text-left th_color">Address</th>
                </tr>
              </thead>
              <tbody>
                <!-- <tr v-show="no_result">
                No results Found
              </tr> -->
                <tr
                  class="mt-2"
                  v-for="item in dataArr"
                  :key="item.id"
                  @click="viewMore(item)"
                >
                  <td>
                    <span v-for="doc in item.documents" :key="doc.id">
                      <img
                        v-if="doc.name === 'Passport Photo'"
                        :src="baseurl + doc.file"
                        alt=""
                        class="image__pp"
                      />
                    </span>
                  </td>
                  <!-- <td > {{ doc.name }} </td> -->
                  <td class="text-uppercase">{{ item.reference_number }}</td>
                  <td>{{ item.name }}</td>
                  <!-- <td>{{ item.email }}</td> -->
                  <td>
                    <span v-if="item.phone_number === null">null</span>
                    <span v-else> {{ item.phone_number }} </span>
                  </td>
                  <td>
                    <span v-if="item.address === null"> null</span>
                    <span v-else>{{ item.address }}</span>
                  </td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
          <nav>
            <ul
              class="
                pagination pagination-md
                d-flex
                justify-content-center
                align-items-center
                mt-5
              "
              style="gap: 20px"
            >
              <li class="page-item" :class="{ disabled: dataObj.total === 0 }">
                <a
                  href="javascript:void(0)"
                  class="page-link"
                  @click="next(dataObj.current_page - 1)"
                >
                  &laquo;
                </a>
              </li>
              <li>
                Showing <span> {{ dataObj.from }} - {{ dataObj.to }} </span> of
                <span> {{ dataObj.total }} </span>
              </li>
              <!-- <li
              class="page-item"
              v-for="page in dataObj.last_page"
              :key="page"
              :class="{active: dataObj.current_page === page }"
            >
              <a
                href="javascript:void(0)"
                @click.prevent="next(page)"
                class="page-link"
              >
                {{ page}}
              </a>
            </li> -->
              <li
                class="page-item"
                :class="{
                  disabled: dataObj.current_page === dataObj.last_page,
                }"
              >
                <a
                  href="javascript:void(0)"
                  class="page-link"
                  @click="next(dataObj.current_page + 1)"
                >
                  &raquo;
                </a>
              </li>
            </ul>
          </nav>
        </div>
      </div>
    </div>

    <div class="merchant-card-container" v-show="merchant_card">
      <div class="merchant__card">
        <div
          class="d-flex align-items-center justify-content-between pt-3 px-3"
        >
          <h5 class="font-weight-bold m-0">{{ merchant.name }}</h5>
          <ion-icon
            name="close-outline"
            @click="merchant_card = !merchant_card"
          ></ion-icon>
        </div>
        <div class="px-3 mb-3">
          <div class="verified">
            <ion-icon name="checkmark-outline"></ion-icon>
            <h5>Verified</h5>
          </div>
        </div>
        <div class="d-md-flex">
          <div class="left__side text-center p-3">
            <span v-for="doc in merchant.documents" :key="doc.id">
              <img
                v-if="doc.name === 'Passport Photo'"
                :src="baseurl + doc.file"
                alt=""
                class="image__pp2"
              />
            </span>
            <div class="icons">
              <ion-icon name="call-outline"></ion-icon>
              <a href="tel:merchant.phone_number" class="">
                <span v-if="merchant.phone_number === null">null</span>
                <span v-else> {{ merchant.phone_number }} </span>
              </a>
            </div>
            <!-- <div class="icons">
              <ion-icon name="mail-outline"></ion-icon>
              <a class="" href="mailto:merchant.email">
                {{ merchant.email }}
              </a>
            </div> -->

            <div class="icons">
              <ion-icon name="location-outline"></ion-icon>
              <p class="">
                <span v-if="merchant.address === null">null</span>
                <span v-else>{{ merchant.address }}, {{ merchant.city }}</span>
              </p>
              <p class="">
                <span v-if="merchant.state === null">null</span>
                <span v-else>{{ merchant.city }}, {{ merchant.state }} </span>
              </p>
            </div>

            <!-- <h6>Documents</h6>
        <div class="d-flex" style="gap:20px">
          <div v-for="doc in merchant.documents" :key="doc.id" >
          <p class="small"> {{ doc.name }} </p>
          <div class="verified">Verified</div>
        </div>
        </div> -->
          </div>

          <div class="right__side">
            <span v-for="doc in merchant.documents" :key="doc.id">
              <img
                v-if="doc.name === 'Shop Photo'"
                :src="baseurl + doc.file"
                alt=""
                class="image__show"
              />
            </span>
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
      baseurl: "https://api.verify.szcmerchant.com/",
      merchant_card: false,
      dataArr: [],
      search: "",
      dataObj: {},
      documents: [],
      merchant: {},
      search: "",
      value: null,
      no_result: false,
    };
  },
  methods: {
    async getKYC(page = 1) {
      this.$axios
        .get("api/kyc", {
          params: {
            page,
            search: this.search,
          },
        })
        .then((res) => {
          this.dataArr = res.data.kyc.data;
          this.dataObj = res.data.kyc;
          if (this.dataArr.length === 0) {
            this.no_result = true;
          } else {
            this.no_result = false;
          }
          // console.log(this.dataArr);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    next(page) {
      this.getKYC(page);
    },
    async viewMore(item) {
      // alert(item.reference_number)
      const new_id = item.reference_number;
      try {
        const res = await this.$axios.get(
          `${this.baseurl}api/kyc/${new_id}/view`
        );
        this.merchant_card = !this.merchant_card;
        // console.log(res.data.kyc);
        this.merchant = res.data.kyc;
      } catch (error) {
        console.log(error);
      }
    },
  },
  async created() {
    this.getKYC();
  },
};
</script>

<style>
.verification_content {
  background-color: #f8f7ff;
  /* padding: 100px;  */
  /* border-radius: 10px; */
  padding: 50px 100px;
}
.verification_content .v-data-table--fixed-header > .v-data-table__wrapper {
  background-color: #f8f7ff;
}
.verification_content .v-data-table > .v-data-table__wrapper > table {
  background-color: #fff;
}
.verification_content .th_color {
  background-color: #f8f7ff !important;
  border-bottom: none !important;
}
.verification_content
  .theme--light.v-data-table
  > .v-data-table__wrapper
  > table
  > thead
  > tr:last-child
  > th {
  border: none;
  box-shadow: none;
}
.image__pp {
  width: 30px;
  height: 30px;
  border-radius: 50%;
  object-fit: cover;
  object-position: top;
}
.image__pp2 {
  width: 100px;
  height: 100px;
  border-radius: 50%;
  margin-bottom: 1rem;
  object-fit: cover;
  object-position: top;
}
.image__show {
  width: 100%;
  /* height: 30; */
  /* border-radius: 50%; */
  object-fit: cover;
  object-position: top;
}
.merchant-card-container {
  background: #01000564;
  z-index: 999;
  position: fixed;
  top: 0;
  left: 0;
  height: 100vh;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: center;
}
.merchant__card {
  width: 30%;
  background: #fff;
  box-shadow: 0px 0px 1px 1px rgba(0, 0, 0, 0.05);
  border-radius: 3px;
  position: relative;
}
.merchant-card-container ion-icon {
  font-weight: bold;
  font-size: 36px;
  color: #ff0000;
}
.merchant__card .icons ion-icon {
  font-size: 15px;
  color: #000;
}
.merchant__card .icons {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-top: 10px;
}
.merchant__card .icons a {
  margin: 0;
  font-size: 15px;

  color: #000;
}
.merchant__card .icons p {
  margin: 0;
  font-size: 15px;
}
.verified {
  background-color: #0c680c31;
  border: 1px solid #0c680c31;
  border-radius: 3%;
  /* height: 8rem; */
  /* width: 8rem; */
  display: flex;
  /* width: 30%; */
  align-items: center;
  /* justify-content: center; */
  /* position: absolute;
  top: 32%;
  left: 45%; */
  padding: 0.3rem 0.8rem;
  gap: 10px;
}
.verified ion-icon {
  color: #0c680c;
  font-weight: bold;
  font-size: 1.1rem;
}
.verified h5 {
  margin: 0;
  font-size: 0.8rem;
  font-weight: bold;
  /* margin-top: -1.3rem; */
  color: #0c680c;
}
.btn__search {
  color: #0c680c;
  background: #0c680c31;
  border: 1px solid #0c680c31;
  padding: 0.3rem 0.5rem;
  border-radius: 3px;
  display: flex;
  align-items: center;
  justify-content: center;
}
@media (max-width: 768px) {
  .verification_content {
    padding: 0.6rem 1.5rem;
  }

  .verification_content h1 {
    font-size: 30px;
  }
  .merchant__card {
    width: 80%;
  }
  .image__pp2 {
    width: 80px;
    height: 80px;
    border-radius: 50%;
    /* margin-bottom: 1rem; */
    object-fit: cover;
    object-position: top;
  }
  .image__show {
    width: 100%;
    height: 200px;
    /* border-radius: 50%; */
    object-fit: cover;
    object-position: top;
  }
  .verification_content .search-area {
    width: 100% !important;
  }
}
</style>