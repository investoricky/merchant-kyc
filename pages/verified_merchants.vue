<template>
  <div>
    <div class="verified_merchant_wrap">
      <div class="verification_content">
        <div class="text-center py-3">
          <h1>Verified Merchants</h1>
        </div>
        <div class="table-responsive">
          <v-simple-table fixed-header height="300px">
            <template v-slot:default>
              <thead>
                <tr class="">
                  <th class="text-left th_color">Ref No</th>
                  <th class="text-left th_color">Name</th>
                  <th class="text-left th_color">Email</th>
                  <th class="text-left th_color">Phone No</th>
                  <th class="text-left th_color">Address</th>
                </tr>
              </thead>
              <tbody>
                <tr class="mt-2">
                  <td>ART4253VCFS</td>
                  <td>Excel Graphixz</td>
                  <td>excelgraphixz@gmail.com</td>
                  <td>09088725534</td>
                  <td>no 21 ekpri nsukara off nwaniba</td>
                </tr>
                <tr class="py-2">
                  <td>RTRFW4566GD</td>
                  <td>Ime Akpan</td>
                  <td>ime@gmail.com</td>
                  <td>070227536576</td>
                  <td>no 40 ebenezer street</td>
                </tr>
                <tr class="py-2">
                  <td>sURFW4556GD</td>
                  <td>Ekpe Ekpad</td>
                  <td>ekpe@gmail.com</td>
                  <td>090772511176</td>
                  <td>no 10 imeh uwah street</td>
                </tr>
              </tbody>
            </template>
          </v-simple-table>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.verified_merchant_wrap {
  padding: 100px;
}
.verification_content {
  background-color: #f8f7ff;
  /* border-radius: 10px; */
  padding: 20px;
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

@media (max-width: 768px) {
  .verified_merchant_wrap {
    padding: 10px;
  }
  .verification_content h1 {
    font-size: 30px;
  }
}
</style>