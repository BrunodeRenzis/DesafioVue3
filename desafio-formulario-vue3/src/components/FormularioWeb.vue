<template>
<div class="contenedor">
  <form action="" @submit.prevent="agregar" id="formulario">
      <div class="contenedorCamposForm">
        <div class="contenedor separador">
            <label for="name">Nombre</label>
            <input type="text" placeholder="Ingrese su nombre" :value="name" @input="(e)=>onInput(e,'name')" id="name" required>
        </div>

        <div class="contenedor separador">
            <label for="email">Email</label>
            <input type="email" placeholder="Ingrese su email" :value="email" @input="(e)=>onInput(e,'email')" id="email" required>
        </div>

        <div class="contenedor separador">
            <label for="telefono">Teléfono</label>
            <input type="number" placeholder="Ingrese su celular" :value="number" @input="(e)=>onInput(e,'number')" id="number" required>
        </div>
        
        <div class="contenedor separador">
            <label for="password">Password</label>
            <input type="password" placeholder="Ingrese su contraseña" :value="editedPassword" id="password" required>  
        </div>

      </div>
      
      <p v-if="editedPassword && !passwordHasNumbers" style="color:red;">No se ha ingresado un dígito en la contraseña</p>
      <select name="" id="" @change="(e)=>onInput(e,'pedido')">
            <option selected></option>
            <option v-for="producto in listaProductos" :value="producto.nombre" :key="producto.id" id="pedido">{{producto.nombre}}</option>
      </select>
      <input @click="agregar(producto.nombre)" type="submit" value="Agregar">    
  </form>
 <tabla-pedidos :datos="this.listaClientes"/>
</div>    

</template>

<script>
import TablaPedidos from './TablaPedidos.vue';
export default {
    name: 'FormularioWeb',
    components:{TablaPedidos},
    data(){
        return{
            name: '',
            email: '',
            number:'',
            pedido:'',
            editedPassword: null,
            listaClientes:[
                
            ],
            listaProductos: [
                {
                    id: 1,
                    nombre: 'Chegusan De Milanga'
                },
                {
                    id: 2,
                    nombre: 'Ignacios con cheddar'
                },
                {
                    id: 3,
                    nombre: 'Sopita paraguaya papá!'
                },
                {
                    id: 4,
                    nombre: 'Pastel de papa con mucho queso como dios manda'
                },
            ]
        }
    },

    methods: {
        agregar(){

            let cliente = {
                id: this.listaClientes.length+1,
                name:this.name ,
                email:this.email ,
                number:this.number ,
                pedido:this.pedido 
            } 
            this.listaClientes.push(cliente);
            this.onClean();
            
        },
        //inputName es la variable a guardar
        onInput(event,inputName){
            this[inputName]=event.target.value;
        },

        onClean(){
            this.name='';
            this.email='';
            this.number='';
            this.pedido='';
        }

    },

    computed: {
        passwordHasNumbers(){
            return /\d/.test(this.editedPassword);
        }
    }
}
</script>

<style scoped>

    body{
        background-color: red !important;
    }

    .contenedor{
        display: flex;
        align-items: center;
        justify-content: center;
        width: 100vw;
        max-width: 200vw;
        flex-direction: column;
        background: rgb(2,0,36);
        background: linear-gradient(90deg, rgba(2,0,36,1) 0%, rgba(7,152,104,1) 55%, rgba(0,212,255,1) 100%);
    }

    .separador{
        margin-top: 1%;
    }

    label{
        color: white;
        font-size: 1.2rem;
        font-weight: 400;
    }


    form{
        margin-top: 5%;
        display: table;
    }

    select{
        margin-top: 5%;
    }

    p     { display: table-row;  }
    label { display: table-cell; }
    input { display: table-cell; }

</style>