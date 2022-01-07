<script>
export default /*#__PURE__*/ {
  name: "VueMzcButtonGroup",
  props: {
    value: {
      type: [String, Number, Array],
      default: "",
    },
    options: {
      type: Array,
      default() {
        return [];
      },
    },
    multiple: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      oneSelected: this.value,
      manySelected: this.value,
    };
  },
  methods: {
    change(value) {
      if (this.multiple) {
        if (this.manySelected.includes(value)) {
          const index = this.manySelected.indexOf(value);

          if (index > -1) {
            this.manySelected.splice(index, 1);
          }
        } else {
          this.manySelected.push(value);
        }
        this.$emit("input", this.manySelected);
      } else {
        this.oneSelected = value;
        this.$emit("input", value);
      }
    },
    getActive(value) {
      if (this.multiple) {
        return this.manySelected.includes(value) ? true : false;
      } else {
        return this.oneSelected == value;
      }
    },
  },
};
</script>

<template>
  <div class="vue-mzc-button-group">
    <button
      class="vue-mzc-button-group__button"
      :class="
        getActive(option.value) ? 'vue-mzc-button-group__button--active' : ''
      "
      v-for="option in options"
      :key="option.id"
      type="button"
      @click="change(option.value)"
    >
      {{ option.title }}
    </button>
  </div>
</template>

<style>
:root {
  --vue-mzc-button-group-padding: 16px;
  --vue-mzc-button-group-height: 32px;
  --vue-mzc-button-group-border-width: 1px;
  --vue-mzc-button-group-border-radius: 6px;
  --vue-mzc-button-group-primary-color: #0075ff;
  --vue-mzc-button-group-background-color: #ffffff;
}
.vue-mzc-button-group {
  display: flex;
}
.vue-mzc-button-group__button {
  cursor: pointer;
  padding-left: 16px;
  padding-right: 16px;
  padding-left: var(--vue-mzc-button-group-padding);
  padding-right: var(--vue-mzc-button-group-padding);
  display: block;
  height: var(--vue-mzc-button-group-height);
  font-size: 1em;
  font-weight: 700;
  color: #0075ff;
  color: var(--vue-mzc-button-group-primary-color);
  background-color: #ffffff;
  background-color: var(--vue-mzc-button-group-background-color);
  border-width: 1px;
  border-width: var(--vue-mzc-button-group-border-width);
  border-color: #0075ff;
  border-color: var(--vue-mzc-button-group-primary-color);
  border-style: solid;
  transition: color 0.25s ease-in-out, background-color 0.25s ease-in-out,
    border-color 0.25s ease-in-out;
}
.vue-mzc-button-group__button:first-child {
  border-top-left-radius: 6px;
  border-bottom-left-radius: 6px;
  border-top-left-radius: var(--vue-mzc-button-group-border-radius);
  border-bottom-left-radius: var(--vue-mzc-button-group-border-radius);
}
.vue-mzc-button-group__button:last-child {
  border-top-right-radius: 6px;
  border-bottom-right-radius: 6px;
  border-top-right-radius: var(--vue-mzc-button-group-border-radius);
  border-bottom-right-radius: var(--vue-mzc-button-group-border-radius);
}
.vue-mzc-button-group__button:not(:first-child) {
  margin-left: -1px;
  margin-left: calc(-1 * var(--vue-mzc-button-group-border-width));
}
.vue-mzc-button-group__button--active {
  color: #ffffff;
  color: var(--vue-mzc-button-group-background-color);
  background-color: #0075ff;
  background-color: var(--vue-mzc-button-group-primary-color);
}
.vue-mzc-button-group__button--active:not(:first-child) {
  border-left-color: #ffffff;
  border-left-color: var(--vue-mzc-button-group-background-color);
}
</style>