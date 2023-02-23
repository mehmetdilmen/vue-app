<template v-if="changedVal">
  <div class="search-container">
    <b-form-select class="selectbox" v-model="changedVal.city">
      <b-form-select-option :value="null" disabled>Şehir</b-form-select-option>

      <b-form-select-option
        v-for="(item, index) in cities"
        :key="index"
        :label="item"
        :value="item"
      />
    </b-form-select>
    <b-form-input
      class="position-input"
      placeholder="Pozisyon"
      v-model="changedVal.query"
    ></b-form-input>
    <b-button class="search-btn" @click="handleFindJob">Ara</b-button>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "Search",
  props: {
    cities: {
      default: [],
    },
    value: {},
  },
  data() {
    return {
      changedVal: JSON.parse(JSON.stringify(this.value)),
    };
  },
  methods: {
    handleFindJob() {
      this.$emit("input", this.changedVal);
    },
  },
  watch: {
    value: {
      immediate: true,
      handler(val) {
        this.changedVal = JSON.parse(JSON.stringify(val));
      },
    },
  },
});
</script>

<style lang="scss">
.search-container {
  display: flex;
  width: 100%;
  margin-top: 50px;
  align-items: center;
  justify-content: center;

  .selectbox {
    width: 300px !important;
    border-radius: 0;
  }

  .selectbox:focus,
  .position-input:focus {
    border-color: purple;
    box-shadow: 0 0 0 0.2rem rgb(211 11 137 / 25%);
  }
  .position-input {
    width: 300px !important;
    border-radius: 0;
  }

  .search-btn {
    background-color: purple;
    border-radius: 0 !important;
  }
}
</style>
