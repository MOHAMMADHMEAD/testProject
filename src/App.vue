<template>
  <v-app>
    <core-filter v-if="owner" />

    <core-toolbar v-if="owner" />

    <core-drawer v-if="owner    "  />

    <core-view />
  </v-app>
</template>
<script>
  export default {
    data()  {
      return {
      owner:localStorage.getItem("owner")
    }
  },
    created(){
      if((this.$router.currentRoute.name=="Login")&&this.owner){
        window.location.href="/"
      }
      console.log(this.$router.currentRoute.name=="Login")
      console.log(this.$router.currentRoute.name)

    },
    metaInfo () {
      return {
        title: 'Vuetify Material Dashboard by CreativeTim'
      }
    }
  }
</script>
<style lang="scss">
@import '@/styles/index.scss';

/* Remove in 1.2 */
.v-datatable thead th.column.sortable i {
  vertical-align: unset;
}
</style>
