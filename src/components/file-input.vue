<template>
  <label :class="className">
    <input type="file" class="input-file" accept="image/*" id="logo" name="logo" @change="input">
    <slot></slot>
  </label>
</template>

<script>
export default {
  name: "FileInput",
  props: {
    value: File,
    label: {
      type: String,
      default: ""
    },
    className: {
      type: String,
      default: ""
    }
  },
  methods: {
    input(e) {
      this.$emit("input", e.target.files[0]);
    }
  }
};
</script>

<style lang="scss" scoped>
input {
  opacity: 0;
  overflow: hidden;
  position: absolute;
  width: 0.1px;
  height: 0.1px;
  z-index: -1;
}
</style>
