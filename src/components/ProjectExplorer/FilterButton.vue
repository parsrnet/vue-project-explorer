<template>
  <div
    class="filter-button-container"
    v-bind:class="filter.enabled ? 'enabled' : ''"
  >
    <input
      type="checkbox"
      class="checkbox"
      :id="filter.id"
      v-model="filter.enabled"
    />
    <label class="filter-button" :for="filter.id">
      <img
        :src="image(filter.imgSrc)"
        v-bind:alt="filter.altText"
        class="size-32 filter-icon"
      />
      <div class="image-overlay-container">
        <span class="image-overlay-text">{{ filter.name }}</span>
      </div>
    </label>
  </div>
</template>



<script>
// Because we lose context upon building and can't know for sure where the icons will end up,
//  we have to use webpack to create a consistent context to find our images.
const imgs = require.context("./icons");

export default {
  name: "FilterButton",
  props: ["filter"],
  methods: {
    image: (dir) => imgs(`./${dir}`),
  },
};
</script>



<style scoped>
/* VARIABLE OPPORTUNITIES */
.filter-button-container {
  flex: 0 1 32px;
  display: grid;
  place-items: center;
  position: relative;
}

.checkbox {
  display: none;
}

/* VARIABLE OPPORTUNITIES */
.filter-icon {
  display: none;
  display: block;
  margin: auto auto;
  width: 32px;
  height: 32px;
  filter: grayscale(1) blur(2px);

  transition: transform 400ms ease-out;
  transform: none;
}
.enabled .filter-icon {
  display: block;
  filter: drop-shadow(-2px 1px 2px #ccc);
  transform: scale(1.2);
}

/* VARIABLE OPPORTUNITIES */
.image-overlay-container {
  display: grid;
  place-items: center;
  position: absolute;
  top: calc(100% + 1vh);
  left: calc(50% - 75px);
  height: 100%;
  width: 150px;
}

.image-overlay-text {
  font-weight: normal;
  text-align: center;
  text-shadow: -2px 2px 0 #eee;
  padding: 1px 4px 1px 4px;
  background: #6662;
  color: #333;
  font-size: 0.8em;
  transition: font-size 600ms linear;
}
.enabled .image-overlay-text {
  font-weight: bold;
  font-size: 1em;
}

@keyframes bounce-in {
  0% {
    transform: scale(0);
  }
  50% {
    transform: scale(1.5);
  }
  60% {
    transform: scale(1);
  }
  75% {
    transform: scale(1.2);
  }
  85% {
    transform: scale(1);
  }
  100% {
    transform: scale(1.2);
  }
}

.filter-button::after {
  display: none;
}
/* VARIABLE OPPORTUNITIES */
.enabled .filter-button::after {
  display: block;
  background: white center / contain no-repeat url("./icons/checkmark.png");
  content: "";
  width: 16px;
  height: 16px;
  border-radius: 8px;
  border: 1px solid white;

  position: absolute;
  bottom: -8px;
  right: -8px;

  animation: bounce-in 300ms ease-in-out;
  transform: scale(1.2);
}
</style>