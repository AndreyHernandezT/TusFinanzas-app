<template>
    <div id="UserData">
        <h3>{{username}}</h3>
        <div>
            <h3>Fecha: <span>  {{fecha}}  </span> </h3>
            <h3>Ingreso: <span>  {{ingreso}}  </span> </h3>
            <h3>Egreso: <span>  {{egreso}} </span> </h3>
            <h3>saldo Actual: <span>  {{saldo_actual}}  </span> </h3>
            
        </div>

    </div>
</template>

<script>
import axios from 'axios';
export default {
    name: 'UserData',
    data: function (){
        return {
            username: "",
            fecha: 1/1/1300,
            ingreso: 0,
            egreso: 0,
            saldo_actual: 0,

        }
    },
    
    created: function(){
        this.username = this.$route.params.username
        
        let self = this
        axios.get("http://127.0.0.1:8000/user/resumen/" + this.username)
            .then((result) => {
                self.fecha = result.data.fecha
                self.ingreso = result.data.ingreso
                self.egreso = result.data.egreso
                self.saldo_actual = result.data.saldo_actual

            })
            .catch((error) => {
                alert("ERROR Servidor");
            });     
    }
}
</script>


<style>
    #UserData{
        width: 100%;
        height: 100%;
        display: flex;
        flex-direction: column;
        justify-content: center;    
        align-items: left;
        text-align: left;
        background-image: url('~@/assets/fondo.png');
        background-size:100%;
        min-height: 70vh;

    }
    #UserData h3{
        font-size: 25px;
        color: #283747;
    }
    #UserData span{
        color: #F58634;
        font-weight: bold;
        font-size: 25px;
    }

</style>