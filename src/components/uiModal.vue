<template>
    <div class="modal" v-if="isOpen">
      <div class="modal-content">
        <slot></slot>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'ui-modal',
    data() {
      return {
        isOpen: false,
      };
    },
    methods: {
      openModal() {
        this.isOpen = true;
      },
      closeModal() {
        this.isOpen = false;
      },
    },
  };
  </script>
<style scoped lang="stylus">
.modal
    position: fixed
    top: 0
    left: 0
    width: 100%
    height: 100%
    background-color: rgba(0, 0, 0, 0.5) /* Fundo semi-transparente */
    display: flex
    justify-content: center
    align-items: center
    z-index: 1000 /* Certifique-se de que o modal esteja acima de outros elementos */

.modal-content
    background-color: #fff
    padding: 20px
    border-radius: 5px
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2)
    max-width: 80%

/* Estilos para o botão de fechar */
.modal-close
    background-color: #f44336
    color: white
    border: none
    border-radius: 3px
    padding: 5px 10px
    cursor: pointer
    position: absolute
    top: 10px
    right: 10px






</style>