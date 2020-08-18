<template>
  <div id="wrapper">
    <Header />
    <Navbar :navlinks="navlinks" />
    <main>
      <div class="container">
        <nuxt />
      </div>
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/Header'
import Footer from '@/components/Footer'
import Navbar from '@/components/Navbar'
export default {
  components: {
    Header,
    Footer,
    Navbar,
  },

  data () {
    return {
      navlinks: [
        { url:'index', title:'Главная' },
        { url:'select', title:'Список' },
        { url:'popup', title:'Popup' },
      ],
    }
  },

}

</script>

<style>

#wrapper {
  max-width: 1200px;
  margin: 10px auto;
  background-color: #f0f0f0;
  border-radius: 15px;
  padding: 15px;
}

</style>
