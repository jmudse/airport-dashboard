<template>
  <div class="dashboard container">
    <Header />
    <div class="container mrgnbtm">
          <div class="row">
            <div class="col-md-8 mt-4">
                <AddPlane @addPlane="addPlane($event)" />
            </div>
          </div>
    </div>
    <div class="row mrgnbtm">
        <Planes @launchModal="launchModal($event)" v-if="planes.length > 0" :planes="planes"/>
    </div>
    <UpdatePlane @updatePlane="updatePlane($event)" @deletePlane="deletePlane($event)" :key="selectedPlane._rev"
      v-bind:planeid="selectedPlane._id || ''"
                 v-bind:planerev="selectedPlane._rev || ''"
                 v-bind:planenumber="selectedPlane.planeObject.plane_number || ''"
                 v-bind:planedeparture="selectedPlane.planeObject.departure || ''"
                 v-bind:planedestination="selectedPlane.planeObject.destination || ''"
                 v-bind:planestatus="selectedPlane.planeObject.status || ''"
    />
  </div>
</template>

<script>
import AddPlane from './AddPlane.vue'
import Planes from './Planes.vue'
import UpdatePlane from './UpdatePlane'
import { getAllPlanes, addPlane, updatePlane, deletePlane} from '../services/planeServices'

export default {
  name: 'Dashboard',
  components: {
    UpdatePlane,
    AddPlane,
    Planes
  },
  data() {
      return {
          planes: [],
          numberOfPlanes: 0,
          selectedPlane: {
            "_id": "defualt",
            "_rev": "1-defualt",
            "planeObject": {
              "plane_number": "defualt",
              "departure": "defualt",
              "destination": "defualt",
              "status": "defualt"
            }
          }
      }
  },
  methods: {
    getAllPlanes() {
      getAllPlanes().then(response => {
        console.log(response)
        this.planes = response
        this.numberOfPlanes = this.planes.length
      })
    },
    addPlane(data) {
      console.log('adding plane: ', data)
      addPlane(data).then(response => {
        console.log(response);
        this.getAllPlanes();
      });
    },
    launchModal(data){
      console.log('Launching modal with:', data);
      this.selectedPlane = data;
      // changing the selectedPlane object reloads the component, so the modal won't launch until the next tick
      this.$nextTick(()=>{
        this.$bvModal.show('update-modal');
      });
    },
    updatePlane(data){
      console.log('updating with:', data);
      this.$bvModal.hide('update-modal');
      updatePlane(data).then(response => {
        console.log(response);
        this.getAllPlanes();
      });
    },
    deletePlane(data){
      console.log('Deleting with:', data);
      this.$bvModal.hide('update-modal');
      deletePlane(data).then(response => {
        console.log(response);
        this.getAllPlanes();
      });
    }
  },
  mounted () {
    this.getAllPlanes();
  }
}
</script>