<template>
    <div id="Personaje">
        <h1>Componente Personaje</h1>
        <p>Id enviado: {{ id }}</p>

        <div id="contenedorTabla">
            <div>
                <table>
                    <tr class="titulos">
                        <td>Nombre</td>
                    </tr>
                    <tr class="valores">
                        <td>{{ nombre }}</td>
                    </tr>
                    <tr class="titulos">
                        <td>Género</td>
                    </tr>
                    <tr class="valores">
                        <td>{{ genero }}</td>
                    </tr>
                    <tr class="titulos">
                        <td>Altura</td>
                    </tr>
                    <tr class="valores" >
                        <td>{{ altura }}</td>
                    </tr>
                    <tr class="titulos">
                        <td>Número de Peliculas</td>
                    </tr>
                    <tr class="valores">
                        <td>{{ numeroPeliculas }}</td>
                    </tr>
                </table>
            </div>
        </div>


    </div>
</template>

<script>
import axios from 'axios';
import { toHandlers } from 'vue';
export default{
    name:'Personaje',
    props:['id'],
    data: function(){
        return{
            nombre:'',
            genero:'',
            altura:'',
            numeroPeliculas:''


        }
    },
    methods:{
        consultarApiEspecifico:function(identificador){
            let url = `https://swapi.dev/api/people/`+identificador;
            axios.get(url)
                .then(respuesta=>{
                    // console.log(respuesta);
                    this.nombre = respuesta.data.name;
                    this.genero = respuesta.data.gender;
                    this.altura = respuesta.data.height;
                    this.numeroPeliculas = respuesta.data.films.length;
                })
                .catch(error=>{
                    console.log(error);
                });
        }
    },
    created(){
        this.consultarApiEspecifico(this.id);
    }
}
</script>

<style scoped>
#Personaje{
    background-color: chocolate;
}

#contenedorTabla{
    text-align: center;
    display: flex;
    justify-content: center;
}

.titulos{
    background-color: gray;
    color: yellow;
}

.valores{
    background-color: black;
    color: white;
}

</style>