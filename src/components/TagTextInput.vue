<template>
  <label id="container" for="text-input">
    <span class="tag">Test</span>
    <input type="text" id="text-input" rows="1" maxLength="12" />
  </label>
</template>



<script>
export default {
  name: "TagTextInput",
  methods: {
    doCheckTags(ev) {
      let newValue = ev.target.value;

      if (newValue.indexOf("test") >= 0) {
        this.$refs[
          "textArea"
        ].innerHTML += `<span class="tag">${newValue}</span>`;
      }
    },
  },
};
</script>



<style scoped>
span.tag {
  color: #f00;
}
#container {
  display: block;
  width: fit-content;
  margin: 0 auto;
  padding: 1px 2px;
  border: 2px inset rgba(195, 195, 195);
  background: rgb(255, 255, 255);
  cursor: text;
  border-image: initial;
}
#text-input {
}
#text-input:focus {
}
</style>