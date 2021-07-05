<template>
        <div>
            <Header />
                <div class="container">
                    <form action="" class="form-horizontal">
                        <div class=form-group left">
                            <label for="" class="control-label col-sm-2">ID_USUARIO</label>
                            <div class="col-sm-10">
                                <input type="text" class="form-control" name="ID_USUARIO" id="ID_USUARIO" v-model="form.ID_USUARIO">
                            </div>
                            </div>
                    <div class="form-group left">
                       <label for="" class="control-label col-sm-2">ID_PERIODO</label>
                       <div class="col-sm-10">
                          <input type="text" class="form-control" name="ID_PERIODO" id="ID_PERIODO" v-model="form.ID_PERIODO">
                       </div>
                    </div>
                    <div class="form-group left row">
                      <div class="col">
                            <label for="" class="control-label col-sm-3">NOMBRE</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="NOMBRE" id="NOMBRE" v-model="form.NOMBRE">
                            </div>
                        </div>
                        <div class="col">
                          <label for="" class="control-label col-sm-5">OBJETIVO_GENERAL</label>
                          <div class="col-sm-7">
                              <input type="text" class="form-control" name="OBJETIVO_GENERAL" id="OBJETIVO_GENERAL" v-model="form.OBJETIVO_GENERAL">
                          </div>
                        </div> 
                    </div>
                    <div class="form-group left row">
                         <div class="col">
                            <label for="" class="control-label col-sm-2">COMPETENCIA</label>
                            <div class="col-sm-7">
                                <input type="text" class="form-control" name="genero" id="COMPETENCIA" v-model="form.COMPETENCIA">
                            </div>
                          </div>
                         <div class="col">
                              <label for="" class="control-label col-sm-2">TEMARIO</label>
                              <div class="col-sm-7">
                                  <input type="text" class="form-control" name="TEMARIO" id="TEMARIO" v-model="form.TEMARIO">
                              </div>
                        </div>
                    </div>
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">AUTORIZADA</label>
                       <div class="col-sm-4">
                          <input type="text" class="form-control" name="AUTORIZADA" id="AUTORIZADA" v-model="form.AUTORIZADA">
                                </div>
                        </div>
                    </div>
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">ID_ORGANIGRAMA</label>
                       <div class="col-sm-4">
                          <input type="text" class="form-control" name="ID_ORGANIGRAMA" id="ID_ORGANIGRAMA" v-model="form.ID_ORGANIGRAMA">
                                </div>
                        </div>
                    </div>
                    <div class="form-group left">
                        <label for="" class="control-label col-sm-2">NO_CREDITOS</label>
                       <div class="col-sm-4">
                          <input type="text" class="form-control" name="NO_CREDITOS" id="NO_CREDITOS" v-model="form.NO_CREDITOS">
                       </div>
                    </div>


                    <div class="form-group">
                      <button type="button" class="btn btn-primary" v-on:click="editar()" >Editar</button>
                      <button type="button" class="btn btn-danger margen" v-on:click="eliminar()" >Eliminar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                        </div>
                    </form>
                 </div>
            <!-- <Footer /> -->
        </div>

</template>
<script>
import Header from '@/components/Header.vue';
//import Footer from '@/components/Footer.vue';
import axios from 'axios';
export default{
    name:"Editar",
    components:{
        Header,
        //Footer,
    },
    data:function(){
        return{
            form:{
                "actividadId" : "",
                "ID_USUARIO" : "",
                "ID_PERIODO" : "",
                "NOMBRE" : "",
                "OBJETIVO_GENERAL" :"",
                "COMPETENCIA" : "",
                "TEMARIO" : "",
                "AUTORIZADA" : "",
                "ID_ORGANIGRAMA" : "",
                "NO_CREDITOS" : "",
                "token" : "" 
            }
        }
    },
    methods:{
        editar(){
            axios.put("http://tabla-actividad.com/actividad", this.form)
            .then( data =>{
                console.log(data);
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        eliminar(){
            var enviar = {
                "actividadId" : this.form.actividadId,
                "token" : this.form.token
            };
            axios.delete("http://tabla-actividad.com/actividad", { header : enviar})
            .then( datos => {
                console.log(datos);
                this.$router.push("/dashboard");
            });
        }
    },
    mounted:function(){
        this.form.actividadId = this.$route.params.id;
        axios.get("http://tabla-actividad.com/actividad?id=" + this.form.actividadId)
        .then( datos =>{
        
            this.form.ID_USUARIO = datos.data[0].ID_USUARIO;
            this.form.ID_PERIODO = datos.data[0].ID_PERIODO;
            this.form.NOMBRE = datos.data[0].NOMBRE;
            this.form.OBJETIVO_GENERAL = datos.data[0].OBJETIVO_GENERAL;
            this.form.COMPETENCIA = datos.data[0].COMPETENCIA;
            this.form.TEMARIO = datos.data[0].TEMARIO;
            this.form.AUTORIZADA = datos.data[0].AUTORIZADA;
            this.form.ID_ORGANIGRAMA = datos.data[0].ID_ORGANIGRAMA;
            this.form.NO_CREDITO = datos.data[0].CREDITO;
            this.form.token = localStorage.getItem("token");
            console.log(this.form);

        })
        
    }
}
</script>
<style scoped>
    .left{
        text-align: left;
    }
</style>