<template>
  <div class="slug-area">
    <b-card class="slug-container">
      <b-row no-gutters>
        <b-col md="3">
          <b-card-img
            :src="this.detail.imageUrl"
            alt="Image"
            class="rounded-0 img-slug"
          ></b-card-img>
        </b-col>
        <b-col md="9">
          <b-card-body
            :title="this.detail.positionName + ' - ' + this.detail.companyName"
          >
            <b-card-text> Açıklama: {{ this.detail.description }} </b-card-text>
            <b-card-text> Adres: {{ this.detail.address }} </b-card-text>

            <b-button href="#" variant="primary">İlana Başvur</b-button>
            <b-button
              :href="`tel:${this.detail?.contactPhone?.number}`"
              variant="primary"
              >Hemen Ara</b-button
            >
            <b-button
              :href="`https://www.google.com/maps/search/?api=1&query=${this.detail?.latitude},${this.detail.longitude}`"
              variant="primary"
              >Harita</b-button
            >
          </b-card-body>
        </b-col>
      </b-row>
    </b-card>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "JobDetailPage",
  data() {
    return {
      detail: [],
      jobId: this.$route.params.slug,
    };
  },
  created() {
    this.fetchDetail();
  },
  methods: {
    async fetchDetail() {
      const data = await this.$axios.$get(
        `https://63f717e7e40e087c95874cab.mockapi.io/api/v1/job_detail?jobId=${this.jobId}`
      );
      this.detail = data[0];
      console.log(this.detail);
    },
  },
});
</script>

<style lang="scss">
.slug-area {
  display: flex;
  align-items: center;
  justify-content: center;
  margin-top: 30px;

  .slug-container {
    margin-left: 30px;
    margin-right: 30px;
  }
}
</style>
