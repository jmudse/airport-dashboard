<template>
    <div class="container">
        <h2>Planes</h2>
        <h4>Click to Update</h4>
        <table class="table table-bordered">
            <thead>
            <tr>
                <th>Plane Number</th>
                <th>Departure</th>
                <th>Destination</th>
                <th>Status</th>
            </tr>
            </thead>
            <tbody>
              <tr v-for="item in planes" :key="item.id"  v-on:click="launchModal(item)">
                  <td>{{ item.planeObject.plane_number }}</td>
                  <td>{{ item.planeObject.departure }}</td>
                  <td>{{ item.planeObject.destination }}</td>
                  <td>{{ item.planeObject.status }}</td>
              </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
    export default {
        name: 'planes',
        props: ['planes'],
        methods:{
          launchModal: function(obj){
            this.$emit('launchModal', obj);
          }
        }

     }
</script>

<style scoped>

  tr:hover td{
    cursor: pointer;
    background: whitesmoke;
  }

  h4 {
    color: grey;
    font-style: italic;
    font-weight: 300;
    font-size: 1.1em;
  }

</style>