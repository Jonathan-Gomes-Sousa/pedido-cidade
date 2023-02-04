<template>
  
   
  
  <CompNavbar :logo="logo_src" :alt="app_name"/>

  <CompBanner/>

<!-- Views -->
  <router-view/>
<!-- /Views -->

  <CompFooter/>

  

</template>
<script>

import CompNavbar from "./components/CompNavbar.vue";
import CompBanner from "./components/CompBanner.vue";
import CompFooter from "./components/CompFooter.vue";
export default{
  name:"App",
  data() {
    return {
      logo_src:"/img/logo.png",
      app_name:"Pedido-Cidade"
    }
  },
  components:{
    CompNavbar,
    CompBanner,
    CompFooter,
    
  }

}

</script>
<style>

</style>
