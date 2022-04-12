<template>
  <div class="container">
    <table v-show="this.datos">
        <thead>
            <th>Id</th>
            <th>Nombre</th>
            <th>Mail</th>
            <th>Teléfono</th>
            <th>Pedido</th>
        </thead>
        <tbody>
            <tr v-for="cliente in this.data" :value="cliente.id" :key="cliente.nombre">
                <td>{{cliente.id}}</td>
                <td>{{cliente.name}}</td>
                <td>{{cliente.email}}</td>
                <td>{{cliente.number}}</td>
                <td>{{cliente.pedido}}</td>
            </tr>
        </tbody>
    </table>
  </div>
</template>

<script>
export default {
    name: 'TablaPedidos',
    props: ["datos"],
    data(){
        return{
            data: this.datos,
        };
    },

};
</script>

<style scoped>
    table{
        margin-top: 5%;
    }

    th,td{
        color: white;
        padding-left: 5rem;
        padding-right: 5rem;
    }
</style>