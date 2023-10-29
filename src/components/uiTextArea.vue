<template>
  <textarea 
  :placeholder="placeholder" 
  :value="value"
  class="text-area"
  @input="updateValue" />
</template>

<script>
export default {
name: 'ui-text-area',

props: {
    placeholder: {
        type: String,
        required: false,
        default: ''
    },
    value: {
        type: String,
        required: false,
        default: ''
    }
},

methods: {
    updateValue(event) {
      this.$emit('input', event.target.value);
    }
  }
}
</script>

<style lang="stylus" scoped>
.text-area
    align-self: stretch 
    height: 89px
    padding-top: 8px 
    padding-left: 8px
    padding-right: 8px 
    border-radius: 4px 
    border: 1px solid rgb(232, 232, 235) 
    flex-direction: column 
    justify-content: flex-start 
    align-items: flex-start 
    display: flex
    
    &::placeholder
        color: #46464A
        font-size: 16px
        font-family: IBM Plex Sans
        font-weight: 400
        line-height: 28.80px
        word-wrap: break-word
</style>

