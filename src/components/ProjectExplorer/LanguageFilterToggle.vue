<template>
  <div
    class="language-filter-toggle"
    :class="language.enabled ? 'enabled' : ''"
  >
    <label :for="language.name" class="image-input-container">
      <input
        type="checkbox"
        v-model="language.enabled"
        :id="language.name"
        style="display: none"
      />
      <img
        :src="icon(language.img)"
        :alt="language.name"
        class="language-image"
      />
      <div class="image-overlay-wrapper">
        <span class="language-name-text">{{ language.displayName }}</span>
      </div>
    </label>
  </div>
</template>



<script>
const iconsDir = require.context("./icons");

export default {
  name: "LanguageFilterToggle",
  methods: {
    icon: (fileName) => iconsDir(fileName),
  },
  props: ["language"],
};
</script>



<style scoped>
.language-filter-toggle {
  --default-size: 64px;

  position: relative;
  width: var(--default-size);
  height: var(--default-size);
}

.image-input-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: absolute;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
}

.language-image {
  --transition-length: 500ms;
  /* DEFAULT STYLING */
  margin: auto;
  height: 100%;
  width: auto;
  transition: transform var(--transition-length) ease-out,
    filter var(--transition-length) linear;

  /* DISABLED STYLING */
  transform: scale(0.75);
  filter: blur(2px) grayscale(1) drop-shadow(1px 1px 1px #333);
}
.enabled .language-image {
  transform: none;
  filter: drop-shadow(1px 1px 1px white);
}

.image-overlay-wrapper {
  display: block;
  width: 100vw;
  height: 100%;

  line-height: var(--default-size);
  text-align: center;
  position: absolute;
  top: 0;
  left: calc(-50vw + var(--default-size) / 2);
  pointer-events: none;

  /* DISABLED */
  transition: transform 400ms ease-in;
  transform: scale(0.75);
}
.enabled .image-overlay-wrapper {
  /* ENABLED */
  transform: scale(1);
}

.language-name-text {
  background: #3333;
  text-shadow: 1px 1px 0 white;
  font-weight: bold;
}
.enabled .language-name-text {
  /* ENABLED */
}
/* CHECKMARK STYLING */
.image-input-container::after {
  --checkmark-radius: 8px;
  --checkmark-border: 1px;
  /* INPUT DISABLED */
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  width: calc(var(--checkmark-radius) * 2);
  height: calc(var(--checkmark-radius) * 2);
  background: white url("./icons/checkmark.png") center / cover no-repeat;
  border: var(--checkmark-border) solid white;
  border-radius: var(--checkmark-radius);

  visibility: hidden;
  animation: pop-out 300ms ease-in;
}
.enabled .image-input-container::after {
  /* INPUT ENABLED */
  display: block;

  animation: pop-in 300ms linear;
  visibility: visible;
}
</style>