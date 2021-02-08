<template>
  <div class="editor-menu">
    <MenuButton :list="listSize"
                :value="size"
                :textButton="'Size'"
                :attribute="attribute.size"
                @changeValue="clickButtonSize"
    />
    <MenuButton :list="listColor"
                :value="color"
                :textButton="'Color'"
                :attribute="attribute.color"
                @changeValue="clickButtonColor"
    />
    <MenuButton :list="listColor"
                :value="bg"
                :textButton="'Background'"
                :attribute="attribute.bg"
                @changeValue="clickButtonBg"
    />
    <button class="editor-button" @click="showJSON">Show JSON</button>
  </div>
</template>

<script>
import MenuButton from "@/components/Editor/Menu/MenuButton";

export default {
  name: "Menu",
  components: {MenuButton},
  props: {
    textJSON: {
      type: Array,
      default: () => []
    }
  },
  data() {
    return {
      attribute: {
        size: 'fontSize',
        color: 'foreColor',
        bg: 'backColor'
      },
      size: 3,
      color: '#000000',
      bg: '#000000',
      listColor: [
        {
          text: 'Black',
          value: '#000000'
        },
        {
          text: 'White',
          value: '#FFFFFF'
        },
        {
          text: 'Red',
          value: '#FF0000'
        },
        {
          text: 'Blue',
          value: '#0000FF'
        },
        {
          text: 'Green',
          value: '#008000'
        }
      ],
      listSize: [
        {
          text: '10',
          value: 1
        },
        {
          text: '13',
          value: 2
        },
        {
          text: '16',
          value: 3
        },
        {
          text: '18',
          value: 4
        },
        {
          text: '24',
          value: 5
        },
        {
          text: '32',
          value: 6
        },
        {
          text: '48',
          value: 7
        }
      ]
    }
  },
  methods: {
    clickButtonSize(value) {
      this.size = value;
      this.checkIsDouble();
    },
    clickButtonColor(value) {
      this.color = value;
      this.checkIsDouble();
    },
    clickButtonBg(value) {
      this.bg = value;
      this.checkIsDouble();
    },
    showJSON() {
      this.$emit('showJSON')
    },
    checkIsDouble() {
      let isDouble = false;
      let obj = {
        text: '',
        size: this.getSize() + 'px',
        color: this.getColor()
      }

      if (!this.textJSON.length) {
        this.$emit('addObjectToJson', obj);
      } else {
        for (let key of this.textJSON) {
          if (key.size === obj.size || key.color === obj.color) {
            isDouble = true;
            return false;
          }
        }
        if (!isDouble) this.$emit('addObjectToJson', obj);
        isDouble = false;
      }
    },
    getSize() {
      for (let key of this.listSize) {
        if (key.value === this.size) return key.text
      }
    },
    getColor() {
      for (let key of this.listColor) {
        if (key.value === this.color) return key.text
      }
    }
  }
}
</script>
