<template src="./SlideContent.html"></template>
<style scoped lang="scss" src="./SlideContent.scss"></style>

<script>
import SlideForm from '../SlideForm/SlideForm.vue';

export default {
  name: 'SlideContext',
  components: {
    SlideForm
  },
  data() {
    return {
      heading: 'Aligning our product',
      subtitle: 'Since 2017',
      text: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce euismod, velit at hendrerit fermentum, tellus odio dignissim arcu, non bibendum velit enim eu ex. Sed et nisl euismod, laoreet enim sed, efficitur velit. Sed eu semper risus.',
      headingFontSize: 60,
      subtitleFontSize: 50,
      textFontSize: 36,
      headingFontSizes: [60, 50, 42],
      subtitleFontSizes: [50, 36, 28],
      textFontSizes: [36, 32, 28, 24, 21, 18],
      textFontSizeIndex: 0,
      headingFontSizeIndex: 0,
      subtitleFontSizeIndex: 0,
      textMaxHeight: 500,
      subtitleMaxHeight: 100,
      headingMaxHeight: 180,
      error: {
        slideSubtitle: false,
        slideHeading: false,
        slideText: false
      }
    };
  },
  watch: {
    heading(newValue, oldValue) {
      this.adjustFontSize('slideHeading', newValue < oldValue, this.headingMaxHeight, 'headingFontSizeIndex', 'headingFontSize', 'headingFontSizes');
    },
    subtitle(newValue, oldValue) {
      this.adjustFontSize('slideSubtitle', newValue < oldValue, this.subtitleMaxHeight, 'subtitleFontSizeIndex', 'subtitleFontSize', 'subtitleFontSizes');
    },
    text(newValue, oldValue) {
      this.adjustFontSize('slideText', newValue < oldValue, this.textMaxHeight, 'textFontSizeIndex', 'textFontSize', 'textFontSizes');
    }
  },
  methods: {
    adjustFontSize(refName, decreaseCondition, maxHeight, indexName, sizeName, sizesArrayName) {
      const el = this.$refs[refName];
      if (el) {
        let height = el.clientHeight;
        const sizesArray = this[sizesArrayName];
        let index = this[indexName];

        while (height < maxHeight - 15 && index > 0 && decreaseCondition) {
          index--;
          this[indexName] = index;
          this[sizeName] = sizesArray[index];
          el.style.fontSize = this[sizeName] + 'px';
          height = el.clientHeight;
        }

        while (height > maxHeight - 15 && index < sizesArray.length - 1 && !decreaseCondition) {
          index++;
          this[indexName] = index;
          this[sizeName] = sizesArray[index];
          el.style.fontSize = this[sizeName] + 'px';
          height = el.clientHeight;
        }
        this.error[refName] = index === sizesArray.length - 1 && height > maxHeight;
      }
    }
  }
};
</script>
