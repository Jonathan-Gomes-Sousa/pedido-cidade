<template>
    <div>
        
        <form>
            <div style="padding: 0px;margin-top: 11px;">
                
                <div>
                    <div class="container-fluid">
                        <div class="card" id="TableSorterCard">
                            <div class="row">
                                <div class="col-12">
                                    <div class="table-responsive">
                                        <table class="table table-striped table tablesorter" id="ipi-table">
                                            <thead class="thead-dark">
                                                <tr>
                                                    <th class="text-center">#</th>
                                                    <th class="text-center">Cliente</th>
                                                    <th class="text-center">pão</th>
                                                    <th class="text-center ">carne</th>
                                                    <th class="text-center ">opcionais</th>
                                                    <th class="text-center ">Ações</th>
                                                </tr>
                                            </thead>

                                            <tbody class="text-center" >
                                                
                                                <tr v-for="burger in burgers" :key="burger.id" >
                                                    <td>{{ burger.id }}</td>
                                                    <td>{{ burger.nome }}</td>
                                                    <td>{{ burger.pao }}</td>
                                                    <td>{{ burger.carne }}</td>
                                                    <td>
                                                        <ul >
                                                            <li v-for=" (opcional, index) in burger.opcionais" :key="index" >
                                                                {{ opcional }}
                                                            </li>
                                                        </ul>
                                                    </td>
                                                    <td class="text-center align-middle"
                                                        style="max-height: 60px;height: 60px;">
                                                        <select class="form-select" @change="updateBurguer($event, burger.id)">
                                            
                                                                <option v-for="s in status" 
                                                                :key="s.id" 
                                                                :value="s.tipo" 
                                                                :selected="burger.status == s.tipo"
                                                                >
                                                                {{ s.tipo }}
                                                                </option>
                                                            
                                                        </select>
                                                        <button @click="deleteBurger(burger.id)" 
                                                            type="submit" 
                                                            class="btn btnMaterial btn-flat accent btnNoBorders checkboxHover"
                                                            style="margin-left: 5px;"
                                                            >
                                                            <i class="fas fa-trash btnNoBorders" style="color: #DC3545;"></i>
                                                        </button>
                                                    </td>
                                                </tr>
                                                
                                            </tbody>
                                        </table>
                                    </div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
            </div>
        </form>
    </div>
</template>
<script>
export default {
    name:'PedidoView',
    data() {
        return {
            burgers:null,
            burger:null,
            status:[]
        }
    },
    methods:{
        async getPedidos(){
            const req = await fetch("http://localhost:3000/burgers")
            const data = await req.json()

            this.burgers = data
            console.log(this.burgers)
            //rsgatar status
            this.getStatus()
        },
        async getStatus(){
            const req = await fetch("http://localhost:3000/status")
            const data = await req.json()
            this.status = data
        },
        async deleteBurger(id){

            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method: "DELETE"
            })
            const res = await req.json()
            console.log(res)

            this.getPedidos()
        },
        async updateBurguer(event,id){
            const option = event.target.value
            const dataJson = JSON.stringify({status:option})

            const req = await fetch(`http://localhost:3000/burgers/${id}`,{
                method:"PATCH",
                headers:{"Content-Type":"application/json"},
                body:dataJson
            })
            const res= await req.json()
            console.log(res)
        }
    },
    mounted() {
        this.getPedidos()
    },
}
</script>