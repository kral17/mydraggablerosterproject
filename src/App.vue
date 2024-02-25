<template>
  <div>
   <router-view></router-view>
  </div>
</template>

<script>
import HomeView from './views/HomeView.vue'
import MainPage from './components/MainPage.vue'
export default {
  components: {
    HomeView,
    MainPage
  }
}

</script>

<style></style>
