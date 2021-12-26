<script>
export default /*#__PURE__*/ {
  name: "VueMzcButtonGroup", // vue component name
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