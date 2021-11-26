<template>
  <div class="parent">
    <FilterView />
    <TagTextInput />
    <!-- TEST !-->
    <ProjectCardCollection />
  </div>
</template>

<script>
import ProjectCardCollection from "./ProjectExplorer/ProjectCardCollection";
import FilterView from "./ProjectExplorer/FilterView";

import TagTextInput from "./TagTextInput"; // TEST

export default {
  name: "ProjectExplorerComponent",
  components: {
    ProjectCardCollection,
    FilterView,
    TagTextInput, // TEST
  },
};
</script>

<style scoped>
</style>