<template>
  <div class="wrapper">
    <div class="langauge-filter-defaults">
      <span
        class="language-filter-text clickable"
        @click="selectAll('fullstack')"
      >
        Full-Stack
      </span>
      <span
        @click="selectAll('frontend')"
        class="language-filter-text clickable"
      >
        Front End
      </span>
      <span
        @click="selectAll('backend')"
        class="language-filter-text clickable"
      >
        Back End
      </span>
    </div>
    <div class="language-filter-container">
      <LanguageFilterToggle
        v-for="language in languages"
        @toggle="doToggle(language)"
        :key="language.name"
        :language="language"
        class="language-filter-item"
      />
    </div>
  </div>
</template>



<script>
import LanguageFilterToggle from "./LanguageFilterToggle";
const languagesSource = require("./json/languages.json");

export default {
  name: "LanguageFilterContainer",
  components: {
    LanguageFilterToggle,
  },
  data() {
    return {
      languages: languagesSource.map(
        (obj) =>
          Object.assign(
            { ...obj },
            { enabled: true }
          ) /* Adding a mutable property from a static JSON file. */
      ),
    };
  },
  methods: {
    selectAll(type) {
      type = type.toLowerCase();
      for (const lang of this.languages) {
        Object.assign(lang, {
          enabled:
            lang.type === "fullstack" ||
            type === "fullstack" ||
            lang.type === type.toLowerCase(),
        });
      }
    },
  },
};
</script>



<style scoped>
.wrapper {
  overflow: hidden;
  max-width: 100%;
}
.language-filter-container {
  --container-height: 10vh;

  display: flex;
  justify-content: space-evenly;
  align-items: center;
  width: 100%;
  height: var(--container-height);
  background: #666;
}

.language-filter-item {
  flex: 0 1 64px;
}

.clickable {
  --default-color: #5ec2ba;

  text-decoration: 1px underline var(--default-color);
  color: var(--default-color);

  cursor: pointer;
}
.language-filter-text::after {
  display: inline;
  content: " | ";
  color: black;

  cursor: default;
}
</style>
