<template>
  <div>
    <Header />
    <div class="container">
      <table class="table table-hover table-responsive">
        <thead>
          <tr>
            <th scope="col">#</th>
            <th scope="col">Nombre</th>
            <th scope="col">Dni</th>
            <th scope="col">Telefono</th>
            <th scope="col">Correo</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="paciente in ListaPacientes" :key="paciente.PacienteId" v-on:click="editar(paciente.PacienteId)">
            <th scope="row">{{paciente.PacienteId}}</th>
            <td>{{paciente.Nombre}}</td>
            <td>{{paciente.DNI}}</td>
            <td>{{paciente.Telefono}}</td>
            <td>{{paciente.Correo}}</td>
          </tr>
        </tbody>
      </table>
    </div>
    <Footer />
  </div>
</template>
<script>
import Header from "@/components/Header.vue";
import Footer from "@/components/Footer.vue";
import axios from 'axios';
export default {
  name: "Dashboard",
  data(){
      return {
          ListaPacientes:null,
          pagina : 1
      }
  },
  components: {
    Header,
    Footer,
  },
  methods:{
      editar(id){
          this.$router.push('/editar/'+id);
      }
  },
  mounted:function(){ 
      let direccion = "https://deyvis-api.hotelmangomarca.com/api-php/pacientes?page="+this.pagina;
      axios.get(direccion).then(data => {
           this.ListaPacientes = data.data;
      })
  }
};
</script>
<style lang="stylus" scoped></style>