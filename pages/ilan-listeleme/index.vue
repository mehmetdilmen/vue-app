<template>
  <div>
    <Search :cities="getCityData" v-model="searchParams" />
    <template v-if="getFilteredJobList?.length">
      <List
        v-for="item in getFilteredJobList"
        :key="item.jobId"
        :job-item="item"
        @handleJobItemClick="handleJobItem"
      />
    </template>

    <div v-else class="no-found">Aranılan kriterde iş ilanı bulunamadı.</div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "JobListPage",
  data() {
    return {
      list: [],
      searchParams: {
        city: null,
        query: "",
      },
    };
  },
  created() {
    this.fetchJobList();
  },
  methods: {
    async fetchJobList() {
      const data = await this.$axios.$get(
        "https://63f717e7e40e087c95874cab.mockapi.io/api/v1/job_list"
      );
      this.list = data;
    },
    handleJobItem(jobId: any) {
      return this.$router.push(`/ilan-detay/${jobId}`);
    },
  },
  computed: {
    getCityData() {
      const cities = this.list.map(
        (item: { cityName: string }) => item.cityName
      );
      return [...new Set(cities)];
    },

    getFilteredJobList() {
      const { city, query } = this.searchParams;
      let data = this.list;

      if (city) {
        data = data.filter(
          (item: { cityName: string }) => item.cityName === city
        );
      }

      if (query.trim().length) {
        data = data.filter(
          (item: { positionName: string; companyName: string }) => {
            return (
              item.positionName.toLowerCase().includes(query.toLowerCase()) ||
              item.companyName.toLowerCase().includes(query.toLowerCase())
            );
          }
        );
      }

      return data;
    },
  },
});
</script>

<style lang="scss">
.no-found {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;
}
</style>
