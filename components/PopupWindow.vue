<template>
  <!--  Правда клик по модальному окну тоже вызывает его закрытие -->
  <div ref="wrapper" @click="closePopup">

    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header"><h4>{{ title }}</h4></div>
          <div class="modal-content">{{ message }}</div>
          <div name="modal-footer">
            <button @click="closePopup">{{ okTitle }}</button>
          </div>
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

    methods: {
      closePopup() {
        this.$emit( 'hide' )
      },

    },

  }
  
</script>

<style scoped>
.wrapper {
  width: 100%;
  height: 100%;
}
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
  max-width: 400px;
  margin: 0px auto;
  background-color: #fff;
  border-radius: 5px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}
.modal-header {
  background-color: #5533ff;
}
.modal-header h4 {
  font-size: 1.1em;
  color: white;
  margin: 0;
  padding: 5px 15px;
}

.modal-content {
  padding: 5px 15px;
  font-size: 1em;

}
</style>