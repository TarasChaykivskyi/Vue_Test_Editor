<template>
  <div>
    <div class="editor">
      <Menu @showJSON="showJSON" :textJSON="textJSON" @addObjectToJson="addObjectToJson"/>
      <div class="editor-container">
        <div class="editor-field" ref="content" contenteditable></div>
      </div>
    </div>
    <EditorJSON :isJson="isJson"
                :textJSON="textJSON"
                @hideJson="hideJson"
    />
  </div>
</template>

<script>
import Menu from "@/components/Editor/Menu/Menu";
import EditorJSON from "@/components/Editor/Json/EditorJSON";

export default {
  name: "Editor",
  components: {EditorJSON, Menu},
  data() {
    return {
      isJson: false,
      textJSON: []
    }
  },
  methods: {
    showJSON() {
      this.isJson = true
    },
    hideJson() {
      this.isJson = false
    },
    addObjectToJson(obj) {
      obj.text = this.$refs.content.innerText;
      if (obj.text.length > 0) this.textJSON.push(obj);
    }
  }
}
</script>
