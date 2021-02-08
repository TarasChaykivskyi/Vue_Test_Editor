<template>
  <div class="modal-json" v-if="isJson">
    <div class="container-json">
      <pre v-if="textJSON.length">{{ textJSON }}</pre>
      <span v-else>No data!</span>
      <button class="editor-button close-button" @click="hideJSON">&times;</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "EditorJSON",
  props: {
    isJson: {
      type: Boolean,
      default: false
    },
    textJSON: {
      type: Array,
      default: () => []
    }
  },
  methods: {
    hideJSON() {
      this.$emit('hideJson');
    }
  }
}
</script>

<style scoped>

</style>
