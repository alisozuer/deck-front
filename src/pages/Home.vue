<template>
 <div>
  <b-container fluid>
      <b-row class="px-0">
        <b-col cols="7" class="px-0">
          <slide-content></slide-content>
        </b-col>
        <b-col cols="5" class="px-0">
          <slide-photos></slide-photos>
        </b-col>
      </b-row>
    </b-container>
 </div>
</template>

<script>
import SlideContent from '../components/SlideContent/SlideContent.vue';
import SlidePhotos from '../components/SlidePhotos/SlidePhotos.vue';

export default {
  name: 'HomePage',
  components: {
    SlideContent,
    SlidePhotos
  }
}
</script>
