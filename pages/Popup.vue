<template>
  <div>
    <PopupWindow
      okTitle="Закрыть"
    >
      <h2 slot="header">Заголовок модального окна</h2>
      <p slot="content">Простое текстовое сообщение</p>

    </PopupWindow>

  </div>
</template>

<script>
  import PopupWindow from '~/components/PopupWindow'
  export default {
    components: {
      PopupWindow,
    },

  }

</script>

<style>
  button {
    margin-top: 20px;
    color: #fff;
    font-weight: bold;
    text-transform: uppercase;
    border: none;
    background: #0fc3f5;
    transition: .3s;
  }
  h2 {
    margin: 0;
    padding: 3px 15px;
    background-color: #5533ff;
  }
  
</style>