<template>
<div class="text-area-container">
    <textarea 
    :placeholder="placeholder" 
    :value="value"
    class="text-area-container-property"
    @input="updateValue" />
    <input type="file" @change="uploadImage" accept="image/*" style="display: none" ref="imageInput" />
    <img ref="imgUpload" id="uploadedimage"  alt="imagem de arquivo pnj/jpeg/jpg" width="200px"/>
    <button class="text-area-container-property-button" @click="openImageInput()">
        <img :src="buttonState === 'notSent' ? imageFile : sentImageFile"/>
    </button>

</div>
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

data() {
    return {
        imageFile: require('@/assets/Vector.svg'),
        sentImageFile: require('@/assets/Type=cancel.svg'),
        buttonState: 'notSent',
    }
},

methods: {
    updateValue(event) {
      this.$emit('input', event.target.value);
    },
    openImageInput() {
        this.$refs.imageInput.click();
    },
  
    uploadImage(event) {
        this.addImg(event)
		this.$emit("input",  event.target.value)
    },
    addImg(event, base64) {
        let preview = this.$refs.imgUpload
        let src = ''
        if(event) {
            src = base64 ? event : URL.createObjectURL(event.target.files[0])
        } 
        preview.src = src
    },
  }
}
</script>

<style lang="stylus" scoped>
.text-area-container
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
    &-property
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
    
        &:placeholder
            color: #46464A
            font-size: 16px
            font-family: IBM Plex Sans
            font-weight: 400
            line-height: 28.80px
            word-wrap: break-word
        &-button
            width: 30px
            background: #fff
            border:none
            position: absolute;
            left: 94%;
            margin-top: 64px;
            margin-left: 6px;
            cursor pointer

</style>

