<!-- TODO :: CRITICAL
  * Need to implement a better way for handling images.
  * Need to clean up the directories direly before beginning implement next steps of project
  * Figure out where to get data from. Figure out how to do data. Are static assets better (?) Are dynamic, cloud-based assets better (?) Where will I host my JSON (? AWS? Talk to Phil)
  * Implement Nuxtent? https://nuxtent-module.netlify.app/guide/writing/#async-components
    * MARKDOWN FOR:
      * Filter buttons ?
      * Projects / Cards !!
!-->

<!-- TODO :: TEMPLATE
    vbind should be removed and replaced with a database 'eventually'
!-->

<template>
  <div class="parent">
    <div class="header-container">
      <Header />
    </div>
    <div class="project-explorer-container">
      <ProjectExplorerComponent />
    </div>
  </div>
</template>

<script>
import Header from "../layout/Header";
import ProjectExplorerComponent from "../components/ProjectExplorerComponent";

export default {
  name: "Home",
  components: {
    Header,
    ProjectExplorerComponent,
  },
};
</script>

<style scoped>
div {
  display: block;
}
</style>