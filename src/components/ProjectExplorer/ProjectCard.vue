<template>
  <li class="parent" :class="project.imgSrc.length > 0 ? 'img-split' : ''">
    <div class="grid-fill wrapper">
      <div class="grid-fill title-area">
        <header>{{ project.title }}</header>
      </div>
      <div class="grid-fill main-area">
        <main>{{ project.description }}</main>
      </div>
      <div class="grid-fill footer-area">
        <footer>{{ project.footer }}</footer>
      </div>
    </div>
    <div class="grid-fill" v-if="project.imgSrc.length > 0">
      <SmartImage :img="image(project.imgSrc)" :alt="project.alt" />
    </div>
  </li>
</template>



<script>
import SmartImage from "./SmartImage";
const imagesDir = require.context("./images");

export default {
  name: "ProjectCard",
  components: {
    SmartImage,
  },
  props: ["project"],
  methods: {
    image: (path) => imagesDir(`./${path}`),
  },
};
</script>



<style scoped>
.grid-fill {
  display: block;
  width: 100%;
  height: 100%;

  text-align: left;
}

.parent {
  display: grid;
  place-items: start;
  min-height: 20vh;

  background: #eee;
  border-radius: 12px;
  padding: 12px;
}
.parent.img-split {
  grid-template-columns: 1fr minmax(12px, 256px);
}

.wrapper {
  display: grid;
  grid-template-rows: auto 1fr auto;
  list-style: none;
  place-items: start;
  gap: 1em;
}
.img-split .wrapper {
  border-right: 2px dashed black;
}

.wrapper header {
  font-size: 2em;
}

.wrapper main {
  text-indent: 1em;
}

.wrapper footer {
  text-align: center;
  font-size: 0.75em;
}
</style>