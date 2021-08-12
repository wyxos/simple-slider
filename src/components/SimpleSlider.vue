<template>
  <div class="simple-slider" ref="slider">
    <div v-for="n in total" :key="n" v-show="currentSlide === n"
         v-touch:swipe.right="() => navigate('previous')"
         v-touch:swipe.left="() => navigate('next')">
      <slot :name="`slide${n}`"></slot>
    </div>
    <slot name="navigation" v-bind="{showPrevious, showNext, navigate}">
      <button v-if="showPrevious" @click="navigate('previous')">Prev</button>
      <button v-if="showNext" @click="navigate('next')">Next</button>
    </slot>
  </div>
</template>

<script>
export default {
  name: 'SimpleSlider',
  props: {
    scrollTopOnNavigate: {
      type: Boolean,
      default: true
    },
    total: {
      type: Number,
      default: 1
    }
  },
  data () {
    return {
      currentSlide: 1
    }
  },
  computed: {
    showPrevious () {
      return this.currentSlide > 1
    },
    showNext () {
      return this.currentSlide < this.total
    }
  },
  methods: {
    navigate (direction) {
      return this[direction]()
    },
    async previous () {
      if (this.currentSlide === 1) {
        return false
      }

      this.currentSlide--

      this.$emit('previous')

      await this.$nextTick()

      if (this.scrollTopOnNavigate) {
        this.scrollTop(this.$refs.slider.offsetTop)
      }
    },
    async next () {
      if (this.currentSlide === this.total) {
        return false
      }

      this.currentSlide++

      await this.$nextTick()

      this.$emit('next')

      if (this.scrollTopOnNavigate) {
        this.scrollTop(this.$refs.slider.offsetTop)
      }
    },
    scrollTop (offset) {
      window.scrollTo({
        top: offset,
        behavior: 'smooth'
      })
    }
  }
}
</script>
