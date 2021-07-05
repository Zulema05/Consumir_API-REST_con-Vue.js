<template>
    <div>
        <Header/>

            <div class="container izquierda">

                <button class="btn btn-primary" v-on:click="nuevo()" >Nueva actividad</button>
                <br><br>

                <table class="table table-hover">
                <thead>
                    <tr>
                        <th scope="col">ID_ACTIVIDAD</th>
                        <th scope="col">ID_USUARIO</th>
                        <th scope="col">ID_PERIODO</th>
                        <th scope="col">NOMBRE</th>
                        <th scope="col">OBJETIVO_GENERAL</th>
                        <th scope="col">COMPETENCIA</th>
                        <th scope="col">TEMARIO</th>
                        <th scope="col">AUTORIZADA</th>
                        <th scope="col">ID_ORGANIGRAMA</th>
                        <th scope="col">NO_CREDITOS</th>
                    </tr>
                </thead>
                <tbody>
                        <tr v-for="actividad in ListasActividad" :Key="actividad.ActividadId" v-on:click="editar"(actividad.ActividadId)>
                        <th scope="row">{{ actividad.ID_ACTIVIDAD }}</th>
                        <td>{{ actividad.ID_USUARIO }}</td>
                        <td>{{ actividad.ID_PERIODO }}</td>
                        <td>{{ actividad.NOMBRE }}</td>
                        <td>{{ actividad.OBJETIVO_GENERAL }}</td>
                        <td>{{ actividad.COMPETENCIA }}</td>
                        <td>{{ actividad.TEMARIO }}</td>
                        <td>{{ actividad.AUTORIZADA }}</td>
                        <td>{{ actividad.ID_ORGANIGRAMA }}</td>
                        <td>{{ actividad.NO_CREDITOS }}</td>
                        </tr>
                </tbody>
                </table>

            </div>

        <Footer/>
    </div>
</template>
<script>
import Header from '@/components/Header.vue';
import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default {
    name:"Dashboard",
    data(){
        return{
            ListasActividad:null,
            pagina:1
        }
    },
    components:{
        Header,
        Footer
    },
    methods:{
            editar(id){
                this.$router.push('/editar/' +id);
             },
            nuevo(){
                this.$router.push('/nuevo/' +id);
            }
    },
    mounted:function(){
        let direccion  = "http://tabla-actividad.com/actividad" + this.pagina;
        axios.get(direccion).then( data =>{
            this.Listasactividad = data.data;
        })
    }
}
</script>
<style scoped>
    .izquierda{
        text-align: left;
    }
</style>