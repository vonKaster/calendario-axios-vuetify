<template>
  <div>
    <v-layout :wrap="true">
      <v-flex xs12>
        <v-card>
          <v-date-picker
          v-model="fecha"
          class="mt-4"
          fullWidth
          locale="es-AR"
          :min="minimo"
          :max="maximo"
          @change="getDolar(fecha)"
        ></v-date-picker>
        </v-card>

        <v-card color="primary" dark>
          <v-card-text class="display-1 text-center">
            {{valor}}
          </v-card-text>
        </v-card>
      </v-flex>
    </v-layout>
  </div>
</template>

<script>
import HelloWorld from "../components/HelloWorld";
import axios from "axios";
import { mapMutations } from "vuex";

export default {
  name: "Home",

  components: {
    HelloWorld,
  },
  data(){
    return{
      fecha: new Date().toISOString().substring(0, 10),
      minimo: '1984',
      maximo: new Date().toISOString().substring(0, 10),
      valor: null
    }
  },
  methods: {
    ...mapMutations(['mostrarLoading', 'ocultarLoading']),

    async getDolar(dia){
      console.log(dia)
      let fechaInvertida = dia.split(['-']);
      let ddmmyy = fechaInvertida[2]+ '-' +fechaInvertida[1] + '-' + fechaInvertida[0];

      try {
        this.mostrarLoading({titulo:'Cargando', color:'primary'})
        let dolar = await axios.get(`https://mindicador.cl/api/dolar/${ddmmyy}`);
        if(dolar.data.serie.length > 0) {
          this.valor = await dolar.data.serie[0].valor;
        } else {
          this.valor = 'Sin resultados'
        }



      } catch (error) {
        console.log(error);
      } finally {
        this.ocultarLoading()
      }


    }
  },
  created(){
    document.title = "Digicard | Calendario";
    this.getDolar(this.fecha);
  }
};
</script>
