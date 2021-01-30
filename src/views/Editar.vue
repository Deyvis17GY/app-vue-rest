<template>
  <div>
    <Header />
    <div class="container">
       <form action="" class="form-horizonatl">
           <div class="form-group left">
               <label for="nombre" class="control-label col-sm-2">Nombre</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="nombre" id="nombre" v-model="form.nombre">
               </div>
           </div>
           <div class="form-group left">
               <label for="dni" class="control-label col-sm-2">Dni</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="dni" id="dni" v-model="form.dni">
               </div>
           </div>
           <div class="form-group left">
               <label for="correo" class="control-label col-sm-2">Correo</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="correo" id="correo" v-model="form.correo">
               </div>
           </div>
           <div class="form-group left">
               <label for="postal" class="control-label col-sm-2">Codigo Postal</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="postal" id="postal" v-model="form.codigoPostal">
               </div>
           </div>
           <div class="form-group left">
               <label for="telefono" class="control-label col-sm-2">Telefono</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="telefono" id="telefono" v-model="form.telefono">
               </div>
           </div>
           <div class="form-group left">
               <label for="fecha" class="control-label col-sm-2">Fecha Nacimiento</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="fecha" id="fecha" v-model="form.fechaNacimiento">
               </div>
           </div>
            <div class="form-group left">
               <label for="token" class="control-label col-sm-2">Token</label>
               <div class="col-sm-10">
                   <input type="text" class="form-control" name="token" id="token" v-model="form.token">
               </div>
           </div>
           <div class="form-group left">
              <button type="button" class="btn btn-primary" v-on:click="editar()">Editar</button>
              <button type="button" class="btn btn-danger margen">Eliminar</button>
              <button type="button" class="btn btn-dark margen">Salir</button>
           </div>
       </form>
    </div>
    <Footer />
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import axios from "axios";

export default {
  name: "Editar",
  components: {
    Header,
    Footer,
  },
  data: function () {
    return {
     
      form: {
        pacienteId :"",
        nombre: "",
        dni: "",
        correo: "",
        codigoPostal: "",
        genero: "",
        telefono: "",
        fechaNacimiento: "",
        token: ""
      }
    };
  },
  methods:{
      editar(){
          var optionAxios = {
            headers: {
                'Content-Type': 'application/x-www-form-urlencoded'
            }
        }
          axios.put("https://deyvis-api.hotelmangomarca.com/api-php/pacientes",this.form,optionAxios).
          then(data => {
              console.log(data);
          })
      }
  },
  mounted: function () {
    this.form.pacienteId = this.$route.params.id;
    axios.get("https://deyvis-api.hotelmangomarca.com/api-php/pacientes?id=" +this.form.pacienteId)
      .then((data) => {

        this.form.nombre = data.data[0].Nombre;
        this.form.dni = data.data[0].DNI;
        this.form.correo = data.data[0].Correo;
        this.form.codigoPostal = data.data[0].CodigoPostal;
        this.form.genero = data.data[0].Genero;
        this.form.telefono = data.data[0].Telefono;
        this.form.fechaNacimiento = data.data[0].FechaNacimiento;
        this.form.token = localStorage.getItem("token");
        console.log(this.form);
      

        

      });
  },
};
</script>
<style scoped>
.left{
    text-align: left;
}
</style>