<template>
  <button 
  class="button" 
  :disabled="disabled"
  :class="design"
  @click="handleClick">
    {{ label }}
  </button>
</template>

<script>
export default {
  name: "ui-button",

  props: {
    label: {
      type: String,
      default: ''
    },
    disabled: {
      type: Boolean,
      required: false,
      default: false
		},
    design: {
      type: String,
      required: false,
      default: 'primary'
		},
  },

  methods: {
    handleClick() {
      this.$emit('click')
    }
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="stylus">
.button
  width 100%
  height 100%
  padding-left 24px
  padding-right 24px
  padding-top 12px
  padding-bottom 12px
  border-radius 8px
  overflow hidden
  justify-content center
  align-items center
  display inline-flex
 
  cursor pointer
  &.primary
    width 20%
    height 20%
    color #fff
    background #293EA5
  &.sucess
    width 100%
    height 100%  
    color #fff
    background: #38A96D
  &::disabled
    width 100%
    height 100%
    color: #9D9DA3
    background: #DCDCE1


    

</style>