<template>
  <div>
    <button @click="show">Показать окно</button>
    <PopupWindow 
      ref="popup"
      :okTitle="okTitle" 
      :title="title" 
      :message="message" 
      :show="show" 
    />
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
        this.$refs['popup'].isVisible = true
      },

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