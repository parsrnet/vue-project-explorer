<template>
  <div class="parent">
    <FilterTextListContainer :tags="appliedTags" v-on:delete-tag="deleteTag" />
    <div class="filter-form">
      <label for="filter-text-input">
        Tag Filter:
        <div class="dropdown-wrapper">
          <input
            type="text"
            size="28"
            maxLength="12"
            id="filter-text-input"
            v-model="text"
            :class="validTags.includes(text.toLowerCase()) ? 'exact-match' : ''"
            @keydown.enter="addSearchTag(text)"
          />

          <div class="filter-button-wrapper">
            <input
              type="image"
              id="filter-dropdown-btn"
              v-bind:src="imgs.dropdownIcon"
              alt="Dropdown"
              @click="addSearchTag(text)"
              class="filter-icon"
            />
          </div>
          <transition-group tag="div" name="dropdown-anim" class="dropdown">
            <span
              v-for="tag in crossTags"
              v-bind:key="tag"
              @click="addSearchTag(tag)"
              class="dropdown-item"
              >{{ tag }}</span
            >
          </transition-group>
        </div>
      </label>
      <span class="span-option" @click="clearAllFilters">Clear All</span>
      <span class="span-option" @click="chooseRandom">Randomize</span>
    </div>
  </div>
</template>



<script>
import FilterTextListContainer from "./FilterTextListContainer";
import { tags as validTags } from "./json/testValidTags.json";

export default {
  name: "FilterText",
  components: {
    FilterTextListContainer,
  },
  data() {
    return {
      appliedTags: [],
      validTags: validTags,
      text: "",
      dropdown: "dropdown",
      imgs: {
        dropdownIcon: require("./icons/dropdown.png"),
        circleClr: require("./icons/circle-clr.png"),
      },
    };
  },
  methods: {
    chooseRandom() {
      // This should eventually choose from a list of templates.
    },
    clearAllFilters() {
      this.appliedTags = [];
    },
    deleteTag(tag) {
      this.appliedTags = this.appliedTags.filter((t) => t !== tag);
    },
    addSearchTag(tag) {
      if (this.validTags.includes(tag) && !this.appliedTags.includes(tag)) {
        this.appliedTags.push(tag);
        this.text = "";
      }
    },
  },
  computed: {
    crossTags() {
      return this.validTags.filter(
        (t) =>
          this.appliedTags.includes(t.toLowerCase()) !== true &&
          t.indexOf(this.text.toLowerCase()) !== -1
      );
    },
  },
};
</script>



<style scoped>
::-webkit-scrollbar {
  width: 12px;
}
::-webkit-scrollbar-track {
  background: #aaa;
  border-radius: 4px;
}
::-webkit-scrollbar-thumb {
  background: #888;
  border-radius: 12px;
}
::-webkit-scrollbar-thumb:hover {
  background: #555;
}

.parent {
  position: relative;
  width: 100%;
}
.dropdown-wrapper {
  display: inline-block;
  position: relative;
}

.exact-match {
  transition: text-shadow 400ms, color 400ms;
  text-shadow: 0 0 4px rgba(123, 218, 0, 0.9);
}

.dropdown-wrapper input[type="text"] {
  border: 1px solid black;
  border-radius: 2px;

  background: #ccc;
}

.dropdown {
  position: absolute;
  display: none;
  left: 0;
  top: calc(100% - 2px);
  min-width: 100%;
  min-height: 16px;
  max-height: 200px;
  overflow-y: auto;

  box-sizing: border-box;
  box-shadow: 0 8px 16px 0 rgba(0, 0, 0, 0.2);
  z-index: 10;

  background: #ccc;
  border: 1px solid black;
  border-top: none;
}
span.dropdown-item {
  display: block;
  background: #ccc;
  width: 100%;
  min-height: 16px;
  transition: background-color 600ms, opacity 800ms, transform 800ms;
}
span.dropdown-item:hover {
  background: #eee;
}

.dropdown-wrapper input:focus ~ .dropdown,
.dropdown-wrapper input:hover ~ .dropdown,
.dropdown:hover,
.dropdown:focus {
  display: block;
}

.filter-form {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  min-height: 72px;
  width: 100%;
  margin: 0;
}

.filter-text-input {
  flex-grow: 1;
}

.filter-button-wrapper {
  display: block;

  position: absolute;
  top: 2px;
  right: 4px;
}
.filter-icon {
  margin: 0 2px;
  width: 12px;
  height: 12px;
}
#filter-dropdown-btn {
  transform: rotate(270deg);
}

.dropdown-anim-leave-active {
  position: absolute;
}
.dropdown-anim-enter,
.dropdown-anim-leave-to {
  transform: translateX(-100%);
  opacity: 0;
}
.dropdown-anim-move {
  transition: transform 800ms;
}

.span-option {
  display: inline;
  font-size: 0.75em;
  color: #5ec2b9f8;
  text-decoration: underline solid #448f89f8;
  margin-left: 12px;

  cursor: pointer;
}
</style>