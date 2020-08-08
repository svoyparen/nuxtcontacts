<template>
  <div>
    <button @click="show">Показать окно</button>
    <div >
      <PopupWindow okTitle="Закрыть" v-if="this.isVisible">
        <div slot="header" class="header">
          <h4>Заголовок модального окна</h4>
        </div>
        <div slot="content">
          <p><span>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Nihil fugit nam eligendi maiores, soluta sit odit maxime doloribus adipisci dignissimos deleniti. Suscipit voluptatum, eos sit ea nam blanditiis minima ducimus!</span>
          <span>Similique et aut non nemo accusantium soluta, a excepturi. Ab, rem. Incidunt perspiciatis assumenda, distinctio, ullam tenetur repellat delectus nisi corrupti corporis omnis saepe magni quam, esse velit beatae aspernatur.</span>
          <span>Laudantium temporibus labore quae veritatis, ex nulla. Debitis illo illum dolorem. Vel quidem quaerat aperiam, praesentium ipsam at ex molestiae! Quaerat voluptatum quia quae accusamus vero perspiciatis quas earum odit.</span></p>
        </div>
        <div slot="footer">
            <button type="button" @click="hide">
              {{ okTitle }}
            </button>
        </div>
      </PopupWindow>
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
      }

    }

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
  .header {
    margin: 0;
    padding: 5px 15px;
    background-color: #5533ff;
  }
  p {
    padding: 5px 15px;
  }

</style>