<script>
import Vue from 'vue';
import VueMzcButtonGroup from '@/vue-mzc-button-group.vue';
import "./serve.css";

export default Vue.extend({
  name: 'ServeDev',
  components: {
    VueMzcButtonGroup
  },
  data() {
    return {
      oneSelected: 1,
      manySelected: [2, 3],
      options: [
        { id: 1, title: 'VueJS', value: 1, },
        { id: 2, title: 'JavaScript', value: 2, },
        { id: 3, title: 'CSS', value: 3, },
      ]
    }
  },
});
</script>

<template>
  <div id="app">
    <div class="row">
      <vue-mzc-button-group :options="options" v-model="oneSelected" />
    </div>
    <div class="row">
      <vue-mzc-button-group :options="options" multiple v-model="manySelected" />
    </div>
  </div>
</template>