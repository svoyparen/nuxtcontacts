<template>
  <div class="PopupWindow">
    <button @click="show">Показать окно</button>
    <div class="modal-mask" v-if="this.isVisible">
      <div class="modal-wrapper">
        <div class="modal-container">
          <slot name="header" class="modal-header"></slot>
          <slot name="content"></slot>
          <slot name="footer">
            <button type="button" @click="hide">
              {{ okTitle }}
            </button>
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
  width: 300px;
  margin: 0px auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header {
  padding: 0;
  background-color: #5533ff;
}

.modal-header h2 {
  margin: 0;
  padding: 3px 15px;
  color: #42b983;
}
.modal-body {
  margin: 20px 0;
}
</style>