<template></template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "IndexPage",
  created() {
    return this.$router.push(`/ilan-listeleme`);
  },
});
</script>