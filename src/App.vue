<template>
  <div>
    <web-header></web-header>
    <home-page></home-page>
    <web-footer></web-footer>
  </div>
</template>

<script>
import WebHeader from './components/Header/WebHeader.vue'
import HomePage from './components/Page/HomePage.vue'
import WebFooter from './components/Footer/WebFooter.vue'
export default {
  components: {
    WebHeader,
    HomePage,
    WebFooter,
  }
}
</script>
