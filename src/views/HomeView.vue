<template>
    <form id="Formulario" @submit='criarPedido'>
             <hr>
            <div id="container" >
                <CompMessage :msg="msg" v-show="msg"/>
                <div>
                    <div class="camposlabel" >
                        <label class="form-label estiloLabel" >Nome Cliente:</label>
                        <input class="form-control" type="text" v-model="nome">
                    </div>

                    <div class="camposlabel">
                        <label class="form-label estiloLabel" >Escolha o pão:</label>
                        <select class="form-select" v-model="pao">
                            <option  v-for="pao in paes" :key="pao.id" :value="pao.tipo">
                                {{ pao.tipo }}
                            </option>
                        </select>
                    </div>

                    <div class="camposlabel">
                        <label class="form-label estiloLabel" > Escolha o carne:</label>
                        <select class="form-select" v-model="carne">
                            <option v-for="carne in carnes" :key="carne.id" :value="carne.tipo">
                                {{carne.tipo}}
                            </option>
                        </select>
                    </div>

                    <div  class="d-flex flex-row flex-wrap">
                        <div id="opcionais">
                            <div>
                                <label class="form-label estiloLabel" >Escolha o carne:</label>
                            </div>
                            <div class="d-flex flex-row flex-wrap" v-for="opcional in opcionaisData" :key="opcional.id">
                                <input type="checkbox" v-model="opcionais" :value="opcional.tipo">
                                <span  >{{opcional.tipo }}</span>
                            </div>
                        </div>
                    </div>

                    <div class="d-flex justify-content-center" style="margin-top: 15px;">
                        <button class="btn btn-warning btn btn-block bt-criar" type="submit" >Criar Pedido</button>
                    </div>
                </div>
            </div>
        </form>
</template>

<script>

import CompMessage from "../components/CompMessage.vue";
export default {
  name: 'HomeView',
  data() {
    return {
        paes:null,
        carnes:null,
        opcionaisData:null,

        nome:null,
        pao:null,
        carne:null,
        opcionais:[],
        msg:null



    }
  },
  components:{
    CompMessage
  },
  methods:{
    async getingredientes(){
        const req = await fetch("http://localhost:3000/ingredientes")
        const data =await req.json()
        
        this.paes = data.paes
        this.carnes = data.carnes
        this.opcionaisData = data.opcionais
    },
    async criarPedido(e){
        e.preventDefault();
        
        const data ={
            nome:this.nome,
            carne:this.carne,
            pao:this.pao,
            opcionais:Array.from(this.opcionais),
            status:"solicitado",
        }
        const dataJson = JSON.stringify(data)
        const req = await fetch("http://localhost:3000/burgers",{
            method:"POST",
            headers:{"Content-Type":"application/json"},
            body: dataJson
        })
            const res = await req.json()

            this.msg = `Pedido nº${res.id} Realizado com Sucesso`
            setTimeout( () => this.msg ="", 3000)

            this.nome =''
            this.pao= ''
            this.carne =''
            this.opcionais =''
            
    }
  },
  mounted() {
    this.getingredientes()
  },
  
}
</script>

<style>
#container{
    padding: 50px;
}
.estiloLabel{
    font-weight: bold;
    border-left: 4px solid #f9b402;
}
.camposlabel{
    margin-bottom: 12px;
}
#opcionais{
    width: 50%;
    margin-left: 6px;
    margin-bottom: 15px;
    font-weight: bold;
}
.bt-criar{
    color: rgb(255,255,255);
    font-weight: bold;
    margin-top: 12px;
}
</style>
