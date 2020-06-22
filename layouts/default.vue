<template>
  <div id="wrapper">
    <Header />
    <main>
      <div class="container">
        <nuxt />
      </div>
    </main>
    <Footer />
  </div>
</template>

<script>
import Header from '@/components/header'
import Footer from '@/components/footer'
export default {
  components: {
    Header,
    Footer
  }
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
