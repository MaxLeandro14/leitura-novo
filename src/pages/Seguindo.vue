<template>
  <div>
  <q-toolbar style="background: rgb(251, 251, 251); border-bottom: 1px solid #e8e4e4;">
 <q-btn  @click="back" flat round dense icon="keyboard_backspace"/>
<q-toolbar-title class="primary-font" style="font-size: 16px;">
Seguindo
</q-toolbar-title>
  <!--<q-btn flat round dense icon="more_vert" style="color: #00d15a" />-->
</q-toolbar>
    <div class="q-pa-md q-gutter-sm">
      <div class="row">

      </div>
    </div>
  </div>
</template>

<script >
export default {
  name: 'SeguindoPerfil',
  methods: {
    back: function () {
      this.$router.go(-1)
    }
  }
}
</script>
