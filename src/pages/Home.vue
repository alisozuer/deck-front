<template>
 <div>
  <div class="container-fluid">
      <div class="row px-0">
        <div class="col-lg-7 px-0 left-slide">
          <div class="box-slide">
            <slide-context></slide-context>
          </div>
        </div>
        <div class="col-lg-5 px-0 right-slide">
          <div class="line"></div>
          <img class="slide-background" src="@/assets/img/slide.jpg" alt="">
        </div>
      </div>
  </div>
 </div>
</template>

<script>
import SlideContext from '../components/SlideContext.vue'

export default {
  name: 'HelloWorld',
  components: {
    SlideContext
  },
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>
<style lang="scss" scoped>
.left-slide{
  .box-slide{
  padding: 130px 120px;
}
}
.right-slide{
  position: relative;
  min-height: 100vh;
  .slide-background{
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.line{
  position: absolute;
  left: 0;
  top: 0;
  width: 26px;
  background: rgb(182,207,215);
  background: linear-gradient(0deg, rgba(182,207,215,1) 50%, rgba(116,147,160,1) 50%);
  height: 100%;
  }
}
@media only screen and (max-width: 1480px) {
 .left-slide {
  .box-slide{
  padding: 50px 70px;
}
 }
}
@media only screen and (max-width: 992px) {
 .left-slide {
  .box-slide{
  padding: 15px;
 }
 }
}
</style>
