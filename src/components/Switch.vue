<template>
  <div class="wrapper" @click="change" :class="mode">
    <div class="slider">
      <div class="toggle" :class="{toggled: toggle}"></div>
    </div>
    <p>{{ toggle ? 'on' : 'off' }}</p>
  </div>
</template>

<script>

export default {
  props: ["mode"],
  emits: ['change'],
  data() {
    return {
      toggle: true
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
  display inline-flex
  cursor pointer
  align-items center
  p
    width 20px
  .slider
    width 36px
    height 20px
    border-radius 14px
    background white
    position relative
    margin-right 15px
    transition border-color ease-out 300ms
    .toggle
      width 16px
      height 16px
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
      background #8624DB
      .toggle
        background white
  &.borders
    .slider
      border 2px solid #8624DB
      height 22px
      width 38px
      .toggle
        width 14px
        height 14px
    &.dark
      .slider
        border-color white

</style>