<template>
  <div class="simple-slider" ref="slider">
    <div v-for="n in total" :key="n" v-show="currentSlide === n">
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
  mounted () {
    console.log(this.$slots, this.$scopedSlots)
  },
  methods: {
    navigate (direction) {
      return this[direction]()
    },
    previous () {
      if (this.currentSlide === 1) {
        return false
      }

      this.currentSlide--

      this.$emit('previous')

      this.scrollTop()
    },
    next () {
      if (this.currentSlide === this.total) {
        return false
      }

      this.currentSlide++

      this.$emit('next')

      this.scrollTop()
    },
    scrollTop () {
      window.scrollTo({
        top: this.$refs.slider.offsetTop,
        behavior: 'smooth'
      })
    }
  }
}
</script>
