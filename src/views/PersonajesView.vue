<template>
    <div id="PersonajesView">
        <h1>Vista PersonajesView</h1>
        <button v-on:click="buscarPersonajes">Buscar Mas Personajes</button>
        <div class="flex-container">
            <div class="flex-individual" v-for="(personaje,index) in personajes" v-bind:key="index" >
                <a v-on:click="informacionPersonaje(index)">{{ personaje.name }}</a>
            </div>
        </div>


    </div>
</template>

<script>
import axios from 'axios';
export default{
    name: 'PersonajesView',
    data: function(){
        return{
            personajes: [],
            contadorPagina: 1,
        }
    },
    methods:{
        consumoApi:function(pagina){
            let url = `https://swapi.dev/api/people?page=`+pagina;
            axios.get(url)
                .then(respuesta=>{
                    // console.log(respuesta);

                    for(let i=0; i<respuesta.data.results.length; i++){
                        this.personajes.push(respuesta.data.results[i]); 
                    }

                })
                .catch(error=>{
                    console.log(error);
                });
        },
        buscarPersonajes:function(){
            this.contadorPagina+=1;
            this.consumoApi(this.contadorPagina);
        },
        informacionPersonaje:function(identificador){
            let identificadorAjustado = identificador+1;
            this.$router.push(`/personaje/${identificadorAjustado}`);
        },
    },
    created(){
        this.consumoApi(1);
    }
}
</script>

<style scoped>
#PersonajesView{
    background-color: darksalmon;
}

.flex-container {
  display: flex;
  flex-wrap: wrap;
  background-color: black;
}

.flex-individual{
    border: 2px solid white;
    color: yellow;
    padding:2%;
    margin: 1%;
}
</style>