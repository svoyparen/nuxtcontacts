<template>
  <div class="PopupWindow">
    
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <slot name="header" class="modal-header"></slot>
          <slot name="content"></slot>
          <slot name="footer">
          </slot>
        </div>
      </div>
    </div>

  </div>

</template>

<script>
  export default {
    props: {
      title: { type: String, default: 'Popup' },
      message: {type: String, default: 'Message'},
      okTitle: { type: String, default: 'Ok' },
      loading: { type:Boolean, default: false },
    },

/*
    data: ()=> ({
      isVisible: false,
    }),

    methods: {
      show() {
        this.isVisible = true
        console.log(this.isVisible)
      },

      hide() {
        this.isVisible = false
        console.log(this.isVisible)
      },

    },
*/
  }
  
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.7);
  display: table;
  transition: opacity 0.9s ease;
}
.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}
.modal-container {
  max-width: 600px;
  margin: 0px auto;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

</style>