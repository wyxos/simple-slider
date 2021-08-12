<template>
  <div id="app">
    <div style="height: 1300px; background: blue; margin-bottom: 10rem">

    </div>

    <simple-slider :total="3" :scroll-top-on-navigate="false" @next="scrollTo" @previous="scrollTo">
      <template #slide1>
        <div style="height: 2000px; background: red">
          Slide 1
        </div>
      </template>
      <template #slide2>
        <div style="height: 3000px; background: yellow">
          Slide 2
        </div>
      </template>
      <template #slide3>
        <div style="height: 4000px; background: black">
          Slide 3
        </div>
      </template>
      <template #navigation="{showPrevious, showNext, navigate}">
        <button v-if="showPrevious" @click="navigate('previous')">Prev 1111</button>
        <button v-if="showNext" @click="navigate('next')">Next 22222</button>
      </template>
    </simple-slider>
  </div>
</template>

<script>
import SimpleSlider from '@/components/SimpleSlider'

export default {
  components: {
    SimpleSlider
  },
  methods: {
    scrollTo () {
      console.log('navigating')
    }
  }
}
</script>
