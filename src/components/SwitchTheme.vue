<template>
  <div class="wrapper" @click="change" :class="mode">
    <SunIcon :class="{opaque: toggle}" :fill="toggle? 'white' : undefined" />
    <div class="slider">
      <div class="toggle" :class="{toggled: toggle}"></div>
    </div>
    <MoonIcon :class="{opaque: !toggle}" :fill="toggle? 'white' : undefined"/>
  </div>
</template>

<script>
import SunIcon from '@/components/SunIcon.vue'
import MoonIcon from '@/components/MoonIcon.vue'

export default {
  components: {
    SunIcon, MoonIcon
  },
  props: ["mode"],
  emits: ['change'],
  data() {
    return {
      toggle: false
    }
  },
  methods: {
    change() {
      this.toggle = !this.toggle
      this.$emit('change', this.toggle)
    }
  }
}
</script>

<style lang="stylus" scoped>
.wrapper
  display flex
  cursor pointer
  align-items center
  .slider
    width 38px
    height 22px
    border-radius 14px
    border 2px solid #8624DB
    position relative
    margin 0 5px
    transition border-color ease-out 300ms
    .toggle
      width 14px
      height 14px
      background #8624DB
      border-radius 50%
      position absolute
      top 2px
      left 2px
      transition all ease-out 300ms
      &.toggled
        transform translateX(16px)
  &.dark
    .slider
      border-color rgba(white, 0.7)
      .toggle
        background rgba(white, 0.7)

.opaque
  opacity 0.5

</style>