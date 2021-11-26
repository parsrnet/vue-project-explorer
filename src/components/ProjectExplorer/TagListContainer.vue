<template>
  <div class="tag-list-container">
    <!-- FILTER A SIDE | GAP | FILTER B SIDE !-->
    <div class="unapplied-filter-side">
      <TagList
        :tags="unappliedTags"
      />
  </div>
  <div class="applied-filter-side">
    <TagList
      :tags="appliedTags"
      add
    />
  </div>
</template>



<script>
import TagList from "./TagList";
import tagArray from "./json/testValidTags.json";

export default {
  name: "TagListContainer",
  components: {
    TagList,
  },
  computed: {
    unappliedTags() {
      return this.allTags.filter((tag) => !appliedTags.includes(tag));
    },
  },
  data() {
    return {
      allTags: tagArray,
      appliedTags: [],
    };
  },
  methods: {},
};
</script>



<style scoped>
</style>