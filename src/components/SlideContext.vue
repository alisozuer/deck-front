 <template>
  <div class="slide-container">
    <h1 ref="slideHeading" class="slide-heading" :style="{ fontSize: headingFontSize + 'px' }">{{ heading }}</h1>
    <h5 ref="slideSubtitle" class="slide-subtitle" :style="{ fontSize: subtitleFontSize + 'px' }">{{ subtitle }}</h5>
    <p ref="slideText" class="slide-text" :style="{ fontSize: textFontSize + 'px' }">{{ text }}</p>
    <div class="mt-4">
      <b-button variant="light" class="edit-btn" v-b-modal.modal-1>Edit <b-icon-pencil-square/></b-button>
    </div>
<b-modal id="modal-1" title="Edit content" hide-header-close>
  <div class="d-flex flex-column" style="gap:10px">
    <b-form-group
        label="Title:"
      >
      <b-form-textarea
        v-model="heading"
        type="text"
        placeholder="Heading"
        rows="2"
        max-rows="2"
        @input="updateFontSize('slideHeading', headingFontSizes, headingMaxHeight, headingFontSizeIndex)"
    ></b-form-textarea>
      </b-form-group>
      <b-alert variant="danger" v-if="error.slideHeading" show>Header field exceeded</b-alert>
      <b-form-group
        label="Subtitle:"
      >
      <b-form-textarea
        v-model="subtitle"
        type="text"
        placeholder="subtitle"
        rows="2"
        max-rows="2"
        @input="updateFontSize('slideSubtitle', subtitleFontSizes, subtitleMaxHeight, subtitleFontSizeIndex)"
    ></b-form-textarea>
      </b-form-group>
      <b-alert variant="danger" v-if="error.slideSubtitle" show>Subtitle field exceeded</b-alert>
      <b-form-group
        label="Description:"
      >
      <b-form-textarea
        v-model="text"
        placeholder="Enter something..."
        rows="5"
        max-rows="5"
        @input="updateFontSize('slideText', textFontSizes, textMaxHeight, textFontSizeIndex)"
    ></b-form-textarea>
      </b-form-group>
      <b-alert variant="danger" v-if="error.slideText" show>Content area exceeded</b-alert>
    </div>
    <template #modal-footer="{cancel}">
    <b-button @click="cancel">Close</b-button>
    </template>
</b-modal>
  </div>
</template>

<script>
export default {
  name: 'SlideContext',
  data () {
    return {
      heading: 'Aligning our product',
      subtitle: 'Since 2017',
      text:
        'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Fusce euismod, velit at hendrerit fermentum, tellus odio dignissim arcu, non bibendum velit enim eu ex. Sed et nisl euismod, laoreet enim sed, efficitur velit. Sed eu semper risus.',
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
    }
  },
  methods: {
    updateFontSize (refName, fontSizes, maxheight, fontSizeIndex) {
      if (this.$refs[refName]) {
        const el = this.$refs[refName]
        let height = el.clientHeight
        let fontSize = fontSizes[fontSizeIndex]
        while (height > maxheight && fontSizeIndex < fontSizes.length - 1) {
          fontSizeIndex += 1
          fontSize = fontSizes[fontSizeIndex]
          el.style.fontSize = fontSize + 'px'
          height = el.clientHeight
        }
        const lastFontSizeIndex = fontSizes.length - 1
        if (fontSizeIndex === lastFontSizeIndex && height > maxheight) {
          this.error[refName] = true
        } else {
          this.error[refName] = false
        }
        if (refName === 'slideHeading') {
          this.headingFontSizeIndex = fontSizeIndex
        } else if (refName === 'slideSubtitle') {
          this.subtitleFontSizeIndex = fontSizeIndex
        } else if (refName === 'slideText') {
          this.textFontSizeIndex = fontSizeIndex
        }
      }
    }
  },
  created () {
    this.updateFontSize('slideHeading', this.headingFontSizes, this.headingMaxHeight, this.headingFontSizeIndex)
    this.updateFontSize('slideSubtitle', this.subtitleFontSizes, this.subtitleMaxHeight, this.subtitleFontSizeIndex)
    this.updateFontSize('slideText', this.textFontSizes, this.textMaxHeight, this.textFontSizeIndex)
  },
  computed: {
    fontSizes () {
      const el1 = this.$refs.slideText
      const el2 = this.$refs.slideHeading
      const el3 = this.$refs.slideSubtitle
      const fontSize1 = el1 ? window.getComputedStyle(el1).fontSize : 36
      const fontSize2 = el2 ? window.getComputedStyle(el2).fontSize : 60
      const fontSize3 = el3 ? window.getComputedStyle(el3).fontSize : 50

      return {
        textFontSize: parseInt(fontSize1),
        headingFontSize: parseInt(fontSize2),
        subtitleFontSize: parseInt(fontSize3)
      }
    }
  },
  watch: {
    heading (newValue, oldValue) {
      const el = this.$refs.slideHeading
      if (newValue < oldValue && el) {
        let height = el.clientHeight
        while (height < this.headingMaxHeight && this.headingFontSizeIndex > 0) {
          this.headingFontSizeIndex -= 1
          this.headingFontSize = this.headingFontSizes[this.headingFontSizeIndex]
          el.style.fontSize = this.headingFontSize + 'px'
          height = el.clientHeight
        }
      }
    },
    subtitle (newValue, oldValue) {
      const el = this.$refs.slideSubtitle
      if (newValue < oldValue && el) {
        let height = el.clientHeight
        while (height < this.subtitleMaxHeight && this.subtitleFontSizeIndex > 0) {
          this.subtitleFontSizeIndex -= 1
          this.subtitleFontSize = this.subtitleFontSizes[this.subtitleFontSizeIndex]
          el.style.fontSize = this.subtitleFontSize + 'px'
          height = el.clientHeight
        }
        console.log(this.subtitleFontSizeIndex)
      }
    },
    text (newValue, oldValue) {
      const el = this.$refs.slideText
      if (newValue < oldValue && el) {
        let height = el.clientHeight
        while (height < this.textMaxHeight && this.textFontSizeIndex > 0) {
          this.textFontSizeIndex -= 1
          this.textFontSize = this.textFontSizes[this.textFontSizeIndex]
          el.style.fontSize = this.textFontSize + 'px'
          height = el.clientHeight
        }
      }
    }
  }

}
</script>
<style scoped lang="scss">
.edit-btn{
  border: 1px solid #e3e3e3;
  padding: 8px 20px;
}
.slide-container{
  .slide-heading, .slide-subtitle, .slide-text{
  word-wrap: break-word;
  white-space: pre-wrap;
  line-height: 140%;
  color: #1D1C1C;
  }
}
</style>
