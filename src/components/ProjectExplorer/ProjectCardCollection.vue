<template>
  <div class="wrapper">
    <ul class="card-list">
      <ProjectCard
        v-for="project in projects"
        v-bind:key="project.id"
        v-bind:project="project"
        class="test-class"
      />
    </ul>
  </div>
</template>

<!-- REMEMBER: searchByTerm(searchTerm) { return list.filter( (term) => term.indexOf(searchTerm.toLowerCase()) !== -1); } !-->

<script>
import ProjectCard from "./ProjectCard";

export default {
  name: "ProjectCardCollection",
  components: {
    ProjectCard,
  },
  data() {
    return {
      projects: require("./json/projects.json"),
    };
  },
};
</script>

<style scoped>
/* I should experiment with setting variables here, to be set to the ProjectCard template.
   Classes inside that template would then be able to use these variables. */

/* VARIABLES FOR EVERYTHING */
.test-class:not(:last-child) {
  position: relative;
  margin-bottom: 10vh;
}
.test-class:not(:last-child)::before {
  display: block;
  content: "";
  height: 10vh;
  width: 2px;
  background: #000;
  position: absolute;
  bottom: -10vh;
  left: calc(50% - 1px);
}
.test-class:not(:last-child)::after {
  display: block;
  content: "";
  height: 12px;
  width: 12px;
  background: #000;
  position: absolute;
  top: calc(100% + 5vh - 6px);
  left: calc(50% - 6px);
  transform: rotate(45deg);
}

.card-list {
  padding: 0 16px;
}
</style>