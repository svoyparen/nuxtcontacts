<template>
  <div>
    <div class="modal-mask" @click='hide' v-if="this.isVisible">
        <div class="modal-container">
          <div class="modal-header"><h4>{{ title }}</h4></div>
          <div class="modal-content">{{ message }}</div>
          <div>
            <button @click="hide" class="hide-popup">{{ okTitle }}</button>
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
      show: { type: Function },
    },

    data: () => ({
      isVisible: false,
    }),

    methods: {
      async hide( e = {} ) {
        const { target } = e
        if ( target && ( !target.classList.contains('modal-mask') && !target.classList.contains('hide-popup') ) ) {
          console.log(target)
          return
        }
        this.isVisible = false
      },

    }

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
.modal-container {
  max-width: 400px;
  margin: 100px auto;
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
  button {
    margin-top: 10px;
    color: #fff;
    font-weight: bold;
    text-transform: uppercase;
    border: none;
    background: #0fc3f5;
    transition: .3s;
  }

</style>