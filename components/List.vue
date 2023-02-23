<template>
  <div class="list-container">
    <b-list-group>
      <b-list-group-item
        @click="handleJobItemClick(jobItem.jobId)"
        class="flex-column align-items-start item-list"
      >
        <div class="d-flex w-100 justify-content-between">
          <h5 class="mb-1">{{ jobItem.positionName }}</h5>
          <small>{{ jobItem.cityName }}</small>
        </div>

        <p class="mb-1">
          {{ jobItem.companyName }}
        </p>
        <small>{{ jobItem.distance }}</small>
      </b-list-group-item>
    </b-list-group>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "List",
  data() {
    return {};
  },
  props: {
    jobItem: {},
  },

  methods: {
    handleJobItemClick(jobId: number) {
      this.$emit("handleJobItemClick", jobId);
    },
  },
});
</script>

<style lang="scss">
.list-container {
  display: flex;
  width: 100%;
  margin-top: 50px;
  align-items: center;
  justify-content: center;

  .item-list {
    width: 650px !important;
    margin-bottom: -20px;
    cursor: pointer;
  }
}
</style>
