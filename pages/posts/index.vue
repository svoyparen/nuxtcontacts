<template>
  <div class="container">
    <Table
      :items="items"
      @showPopup="openPopup"
      />
      <Popup
        ref="popup"
      />
  </div>
</template>

<script>
  import Table from '~/components/table'
  import Popup from '~/components/popup'
  import axios from 'axios'

  export default {
    components: {
      Table,
      Popup,
    },

    data: () => ({
      items: [],
    }),

    mounted() {
      this.getData()
    },

    methods: {
      getData(args = []) {
        axios.get('https://test.cornapi.ru/blog')
        .then( response => {
          for ( const item in response.data.data.items ){
            console.log( response.data.data.items[item] )
            this.items.push(response.data.data.items[item])
          }
        })
      },

      openPopup(item) {
        this.$refs.popup.setVisible(true)
        this.$refs.popup.setData(item)
      }

    },

    }

</script>

<style>
.container {
  margin: 0 auto;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
  min-width: 1000px;
  background-color: #159159;
}

.title {
  font-family:
    'Quicksand',
    'Source Sans Pro',
    -apple-system,
    BlinkMacSystemFont,
    'Segoe UI',
    Roboto,
    'Helvetica Neue',
    Arial,
    sans-serif;
  display: block;
  font-weight: 300;
  font-size: 100px;
  color: #35495e;
  letter-spacing: 1px;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>
