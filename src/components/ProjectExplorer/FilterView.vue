<template>
  <div class="parent">
    <div class="filter-wrapper">
      <LanguageFilterContainer />
    </div>
    <div class="filter-text-container">
      <FilterText />
    </div>
  </div>
</template>



<script>
import LanguageFilterContainer from "./LanguageFilterContainer";
import FilterText from "./FilterText";

export default {
  name: "FilterView",
  components: {
    LanguageFilterContainer,
    FilterText,
  },
};
</script>



<style scoped>
.parent {
  background-color: #eee;
  margin: 0 auto;

  display: grid;
  grid-template-rows: 1fr 2fr;
  padding-top: 1em;
}
.filter-text-container {
  background: #aaa;
  margin: auto;
}
</style>