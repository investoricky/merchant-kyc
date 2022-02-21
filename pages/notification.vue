<template>
  <div>
    <div class="notification_wrap">
      <div class="">
        <div class="text-center">
          <div class="d-flex justify-content-center">
            <v-img src="/checked.png" lazy-src="/checked.png" />
          </div>
          <h1>Your KYC has been submitted Successfully!!!</h1>
          <p class="fw-bold">Go back to Mobile App.</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style>
.notification_wrap {
  width: 70%;
  margin: 40px auto;
  padding: 100px;
}
.notification_wrap .v-responsive {
  max-width: 200px;
}
@media (max-width: 768px) {
  .notification_wrap {
    width: 100%;
    padding: 40px 10px;
  }
  .notification_wrap h1 {
    font-size: 26px;
  }
  .notification_wrap p {
    font-size: 13px;
  }
}
</style>