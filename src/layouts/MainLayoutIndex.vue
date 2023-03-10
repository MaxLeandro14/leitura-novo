<template>
  <q-layout>
    <router-view />
    <FooterApp />
  </q-layout>
</template>

<script>
import FooterApp from 'layouts/FooterMenu.vue'
export default {
  name: 'MainLayout',
  components: {
    FooterApp
  },
  data () {
    return {
      leftDrawerOpen: false
    }
  }
}
</script>
<style>
.img-menu{
  width: 30px
}
</style>
