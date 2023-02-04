<template>
    <div>
        <nav class="navbar navbar-dark navbar-expand-md bg-dark">
            <div class="container-fluid"><router-link to="/"><a class="navbar-brand" href="#"><img id="logo"  :src="logo" :alt="alt"></a></router-link><button data-bs-toggle="collapse" class="navbar-toggler" data-bs-target="#navcol-1"><span class="visually-hidden">Toggle navigation</span><span class="navbar-toggler-icon"></span></button>
                <div class="collapse navbar-collapse d-xl-flex justify-content-end justify-content-xl-end" id="navcol-1">
                    <ul class="navbar-nav">
                        <li class="nav-item"><router-link to="/"><a class="nav-link" href="">Home</a></router-link></li>
                        <li class="nav-item"><router-link to="/pedido"><a class="nav-link" href=""> Pedidos</a></router-link></li>
                        
                    </ul>
                </div>
            </div>
        </nav>
    </div>
</template>

<script>
export default {
    name:"compNavbar",
    props:["logo","alt"]
}
</script>

<style>
#logo{
    width: 40px;
    height: 40px;
}
</style>