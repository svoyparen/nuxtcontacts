<template>
  <div>
    <button @click="show">Показать окно</button>
      <PopupWindow
          ref="popup"
          :show="show"
          v-on:beforeHide="beforeHide"
          v-on:hidden="hidden"
          >
        <template v-slot:header><div class="modal-header"><h4>Заголовок</h4></div></template>
        <template v-slot:content><div class="modal-content">Содержимое модального окна</div></template>
        <template v-slot:footer><div><button @click="hide" class="hide-popup">Закрыть</button></div></template>
      </PopupWindow>

<!--
    <PopupWindow 
      ref="popup"
      :okTitle="okTitle" 
      :title="title" 
      :message="message" 
      :show="show" 
    />
-->
  </div>
</template>

<script>
  import PopupWindow from '~/components/PopupWindow'
  export default {
    components: {
      PopupWindow,
    },

    data: () => ({
      title: 'Заголовок',
      message: 'Сообщение в модальном окне',
      okTitle: 'Закрыть',
    }),

    methods: {
      show() {
        console.log('beforeShow')
        this.$refs['popup'].loading = true
        setTimeout( this.show2, 3000 )
      },

      show2() {
        this.$refs['popup'].isVisible = true
        this.$refs['popup'].loading = false
      },

      hide() {
        //this.beforeHide()
        this.$emit('hide')
        //this.hidden()
      },
/*
      beforeHide(){
        console.log('beforeHide')
      },

      hidden(){
        console.log('hidden')
      },
*/
    }

  }

</script>

<style scoped>

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