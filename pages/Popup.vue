<template>
  <div>
    <button @click="show">Показать окно</button>
    <div >
      <PopupWindow :okTitle="okTitle" :title="title" :message="message" v-if="this.isVisible" @hide="hide" />

    </div>
  </div>
</template>

<script>
  import PopupWindow from '~/components/PopupWindow'
  export default {
    components: {
      PopupWindow,
    },

    data() {
      return {
        isVisible: false,
        okTitle: 'Close',
        title: 'Всплывающее окно',
        message: 'Сообщение'
      }
    },

    methods: {
      show() {
        this.isVisible = true
        console.log(this.isVisible)
      },

      hide() {
        if( this.isVisible == true ) {
          this.isVisible = false
          console.log(this.isVisible)
        }
      },

    },

  }

</script>

<style>

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