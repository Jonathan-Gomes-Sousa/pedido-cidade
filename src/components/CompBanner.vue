<template>
    <div id="CompBanner" class="d-flex d-lg-flex justify-content-lg-start" >
        <h1 id="CompBanner-text" class="d-flex justify-content-center align-items-center">Faça seu Pedido</h1>
    </div>
</template>

<script>
export default {
    name:"CompBanner"
}
</script>
<style>
#CompBanner{
    background: url('/public/img/burger.jpg') center / cover no-repeat;
    height: 300px;
    width: auto;
}
#CompBanner-text{
    color: rgba(255,255,255,.2);
    font-size: 60px;
    margin-left: 10px;
    
    
}
</style>
