<template>
  <transition-group name="list" tag="ul" class="container">
    <li v-for="tag in tags" v-bind:key="tag" class="tag-item">
      <label :key="uuidv4()" :for="tag">
        {{ tag }}
        <input
          :key="uuidv4()"
          :id="tag"
          type="image"
          class="delete-tag"
          :src="imgs.circle_x"
          alt="delete"
          v-on:click="deleteTag(tag)"
        />
      </label>
    </li>
  </transition-group>
</template>



<script>
const icons = require.context("./icons/");
import { v4 as uuidv4 } from "uuid";

export default {
  name: "FilterTextListContainer",
  data() {
    return {
      imgs: {
        circle_x: icons("./circle-x.png"),
      },
    };
  },
  methods: {
    uuidv4: uuidv4,
    deleteTag(tag) {
      this.$emit("delete-tag", tag);
    },
  },
  props: ["tags"],
};
</script>



<style scoped>
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
  align-items: center;

  margin: 0 auto;
  min-height: 72px;
  padding: 0;
}

.tag-item {
  display: grid;
  place-items: center;
  background-color: lightpink;
  border-radius: 12px;
  height: 28px;
  min-width: 32px;
  padding: 2px 4px;

  margin-right: 16px;
  margin-top: 4px;
  transition: all 1s;
}

.delete-tag {
  margin-left: 0.5em;
  width: 12px;
  height: 12px;
}

.list-enter,
.list-leave-to {
  opacity: 0;
  transform: scale(0.1);
}
.list-leave-active {
  position: absolute;
}
</style>