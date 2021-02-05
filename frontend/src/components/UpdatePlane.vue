<template>
  <b-modal id="update-modal" title="Update Plane">
    <form>
      <div class="row">
          <input type="hidden" class="form-control" v-model="id" name="id" id="update-id" />
          <input type="hidden" class="form-control" v-model="rev" name="rev" id="update-rev" />

        <div class="form-group col-md-6">
          <label htmlFor="exampleInputEmail1">Plane Number</label>
          <input type="text" class="form-control" v-model="planeNumber" name="planenumber" id="update-planenumber" />
        </div>
        <div class="form-group col-md-6">
          <label htmlFor="exampleInputPassword1">Departure</label>
          <input type="text" class="form-control" v-model="departure" name="departure" id="update-departure" />
        </div>
        <div class="form-group col-md-6">
          <label htmlFor="exampleInputEmail1">Destination</label>
          <input type="text" class="form-control" v-model="destination" name="destination" id="update-destination" />
        </div>
        <div class="form-group col-md-6">
          <label htmlFor="exampleInputPassword1">Status</label>
          <input type="text" class="form-control" v-model="status" name="status" id="update-status" />
        </div>
      </div>

    </form>
    <template #modal-footer="{cancel}">
      <!-- Emulate built in modal footer ok and cancel button actions -->
      <b-button variant="secondary" @click="cancel()">
        Cancel
      </b-button>
      <b-button variant="primary" @click="updatePlane()">
        Update
      </b-button>
      <!-- Button with custom close trigger value -->
      <b-button variant="danger" @click="deletePlane()">
       Delete
      </b-button>
    </template>
  </b-modal>
</template>

<script>
  export default {
  name: "UpdatePlane.vue",
  props: ['planeid', 'planerev', 'planenumber', 'planedeparture', 'planedestination', 'planestatus'],
  data() {
    return {
      id: this.planeid,
      rev: this.planerev,
      planeNumber: this.planenumber,
      departure: this.planedeparture,
      destination: this.planedestination,
      status: this.planestatus
    }
  },
    methods: {
      updatePlane(){
        const payload = {
          id: this.id,
          rev: this.rev,
          plane_number: this.planeNumber,
          departure: this.departure,
          destination: this.destination,
          status: this.status
        }
        this.$emit('updatePlane', payload)
      },
      deletePlane(){
        if (confirm('Are you sure you want to delete this plane? This action cannot be undone.')){
          const payload = {
            id: this.id,
            rev: this.rev,
            plane_number: this.planeNumber,
            departure: this.departure,
            destination: this.destination,
            status: this.status
          }
          this.$emit('deletePlane', payload)
        }
      }
    }
  }

</script>

<style scoped>

</style>