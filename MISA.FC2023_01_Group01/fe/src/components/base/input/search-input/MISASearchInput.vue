<template>
  <div
    class="search-input-container"
    :style="styleInputContainer"
    @click="$refs.input.focus()"
    @mouseenter="hoverInput = true"
    @mouseleave="hoverInput = false"
  >
    <input
      class="search-input__input"
      :placeholder="placeholder"
      ref="input"
      @focus="
        () => {
          focusInput = true;
          $emit('input-focus');
        }
      "
      @blur="
        () => {
          focusInput = false;
          $emit('input-blur');
        }
      "
      v-model="searchText"
    />
    <misa-icon
      icon="search"
      scale="0.8"
      tooltip="Tìm kiếm"
      style="position: absolute; top: 0px; right: 10px"
    />
  </div>
</template>

<script>
export default {
  name: "MISASearchInput",
  data() {
    return {
      focusInput: false,
      hoverInput: false,
      searchText: this.modelValue,
    };
  },
  props: {
    width: {
      default: "250px",
    },
    placeholder: {
      default: "Tìm kiếm",
    },
    modelValue: {
      required: true,
    },
  },
  computed: {
    styleInputContainer() {
      return {
        width: this.width,
        minWidth: this.width,
        maxWidth: this.width,
        border: `${this.focusInput ? "2px" : "1px"} solid ${
          this.borderInputColor
        }`,
      };
    },

    borderInputColor() {
      if (this.focusInput) {
        return "var(--primary-btn--focus-background-color)";
      } else if (this.hoverInput) {
        return "var(--primary-btn--hover-background-color)";
      } else {
        return "var(--border-color-default)";
      }
    },
  },
  watch: {
    searchText(newValue) {
      this.$emit("update:modelValue", newValue);
    },
  },
};
</script>

<style scoped>
@import url(./search-input.css);
</style>
