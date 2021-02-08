<template>
  <button class="editor-button"
          id="fontSize"
          :data-attribute="attribute">
    <select class="editor-select"
            v-model="currentValue"
            @change="clickActionBtn($event.target, attribute)">
      <option v-for="(item, index) in list"
              :key="index"
              :value="item.value"
      >{{ item.text }}
      </option>
    </select>
    <label for="fontSize">{{ textButton }}</label>
  </button>
</template>

<script>
export default {
  name: "MenuButton",
  props: {
    list: {
      type: Array,
      default: () => []
    },
    value: {
      type: [Number, String],
      default: ''
    },
    attribute: {
      type: String,
      default: ''
    },
    textButton: {
      type: String,
      default: 'Button'
    }
  },
  data() {
    return {
      currentValue: null
    }
  },
  methods: {
    clickActionBtn(e, element) {
      document.execCommand(element, false, e.value);
      this.$emit('changeValue', this.currentValue);
    }
  },
  mounted() {
    this.currentValue = this.value;
  }
}
</script>

<style scoped>

</style>
