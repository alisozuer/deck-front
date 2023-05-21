<template src="./SlideForm.html"></template>
<style lang="scss" scoped src="./SlideForm.scss"></style>
  
  <script>
  export default {
    name: 'SlideForm',
    props: {
      heading: {
        type: String,
        required: true
      },
      subtitle: {
        type: String,
        required: true
      },
      text: {
        type: String,
        required: true
      },
      error: {
        type: Object,
        required: true
      }
    },
    computed: {
      headingValue: {
        get() {
          return this.heading;
        },
        set(value) {
          this.$emit("update:heading", value);
        }
      },
      subtitleValue: {
        get() {
          return this.subtitle;
        },
        set(value) {
          this.$emit("update:subtitle", value);
        }
      },
      textValue: {
        get() {
          return this.text;
        },
        set(value) {
          this.$emit("update:text", value);
        }
      }
    }
  };
  </script>