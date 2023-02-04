<template>
    <div class="alert alert-success" role="alert">
         {{msg}}
     </div>
</template>

<script>


export default {
  name: 'CompMessage',
  props:{
    msg:String
  }
  
}
</script>
<style scoped>


</style>
