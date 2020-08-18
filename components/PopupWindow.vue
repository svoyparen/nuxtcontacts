<template>
  <div>
      <slot name="popup">
        <div class="modal_mask" v-if="this.loading">
          <div class="modal-container">
            <div class="preloader">&nbsp;</div>
          </div>
        </div>
            
        <div class="modal-mask" @click='hide' v-if="this.isVisible">
            <div class="modal-container">
              <slot name="header"></slot>
              <slot name="content"></slot>
              <slot name="footer" :hide="hide"></slot>

<!--
          <div class="modal-header"><h4>{{ title }}</h4></div>
          <div class="modal-content">{{ message }}</div>
          <div>
            <button @click="hide" class="hide-popup">{{ okTitle }}</button>
          </div>
-->
            </div>
      </div>
      </slot>
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
      loading: false,
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

.preloader {
  position: absolute;
  top: 10%;
  left: 40%;
  width: 150px;
  height: 150px;
  border: 5px solid #eae4ea;
  box-shadow: 0 -2px 2px rgba(0,0,0,.2);
  border-bottom: 5px solid #6ddfca;
  border-radius: 50%;
  animation: loader 3s linear infinite;
}

.preloader:before {
    content: '';
    position: absolute;
    top: 10px;
    left: 10px;
    bottom: 10px;
    right: 10px;
    border: 5px solid #eae4ea;
    box-shadow: 0 -2px 2px rgba(0,0,0,.2);
    border-bottom: 5px solid #d355be;
    border-radius: 50%;
    animation: loader 2s linear infinite;
}

.preloader:after {
    content: '';
    position: absolute;
    top: 22px;
    left: 22px;
    bottom: 22px;
    right: 22px;
    border: 5px solid #eae4ea;
    box-shadow: 0 -2px 2px rgba(0,0,0,.2);
    border-bottom: 5px solid #8c23ec;
    border-radius: 50%;
    animation: loader 1s linear infinite;
}

@keyframes loader
{
    0%
    {
        transform: rotate(0deg);
    }
    100%
    {
        transform: rotate(360deg);
    }
    
}

</style>
