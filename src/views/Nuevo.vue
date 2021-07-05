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
                      <button type="button" class="btn btn-primary" v-on:click="guardar()" >Guardar</button>
                      <button type="button" class="btn btn-dark margen" v-on:click="salir()"  >Salir</button>
                        </div>
                </form>
            </div>
        <!-- <Footer /> -->

    </div>
</template>
<script>
import Header from '@/components/Header.vue'
//import Footer from '@/components/Footer.vue'
import axios from 'axios'; 
export default{
    name:"Nuevo",
    data:function(){
        return{
            form:{
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
    components:{
        Header,
        //Footer
    },
    methods:{
        guardar(){
            this.form.token = localStorage.getItem("token"); 
            axios.post("http://tabla-actividad.com/actividad",this.form)
            .then(data =>{
                console.log(data);
                this.makeToast("Hecho","Actividad creada","success");
                this.$router.push("/dashboard");
            }).catch( e =>{
                console.log(e);
                 this.makeToast("Error","Error al guardar","error");
            })
        },
        salir(){
            this.$router.push("/dashboard");
        },
        makeToast(titulo,texto,tipo) {
            this.toastCount++
            this.$bvToast.toast(texto, {
            title: titulo,
            variant: tipo,
            autoHideDelay: 5000,
            appendToast: true
            })
        }
    }

}
</script>
<style scoped>
.left{
    text-align: left;
}
</style>