<!-- SmartImages are automatically scaled !-->

<template>
  <div class="container">
    <img v-bind:src="img" v-bind:alt="alt" class="inner-image" ref="imgRef" />
    <input
      id="click-to-expand"
      class="image-overlay"
      type="image"
      :src="icon('magnifying_glass.png')"
      @click="expanded = !expanded"
      alt
    />
  </div>
</template>


<script>
const iconsDir = require.context("./icons");

export default {
  name: "SmartImage",
  data() {
    return {
      expanded: false,
    };
  },
  methods: {
    icon: (path) => iconsDir(`./${path}`),
  },
  props: ["img", "alt"],
};
</script>



<style scoped>
.container {
  display: grid;
  place-items: center;
  height: 100%;
  width: 100%;
  position: relative;
}
.inner-image {
  filter: blur(4px);
  width: 80%;
  height: 80%;

  transition: filter 600ms linear;
}
/* VARIABLES */
.image-overlay {
  position: absolute;
  top: calc(50% - 28px);
  left: calc(50% - 28px);

  background: #eeeeee30;
  width: 32px;
  height: 32px;
  padding: 12px;
  border-radius: 4px;
}
.image-overlay:hover {
  background: #ffffff60;
}

.expanded {
  display: none;
}
</style>