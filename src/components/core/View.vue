<template>
  <v-content>
    <div id="core-view">
      <v-fade-transition mode="out-in">
        <router-view />
      </v-fade-transition>
    </div>
    <core-footer v-if="this.$router.currentRoute.name !== 'Maps'&&this.$router.currentRoute.name !== 'Login'" />
  </v-content>
</template>

<script>
export default {
  created(){
    return console.log(this.$router.currentRoute.name)
  },
  metaInfo () {
    return {
      title: 'Vuetify Material Dashboard by CreativeTim'
    }
  }
}
</script>

<style>
#core-view {
  padding-bottom: 100px;
}
</style>
