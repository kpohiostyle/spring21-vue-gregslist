<template>
  <div class="car-details" v-if="state.car">
    <div class="row">
      <div class="col-md-12">
        <div class="card shadow">
          <img class="card-img-top" :src="state.car.imgUrl" alt="">
          <div class="card-body">
            <h4 class="card-title">
              something else
            </h4>
            <p class="card-text">
              Make: {{ state.car.make }} | Model: {{ state.car.model }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <button type="button" class="btn btn-danger" @click="deleteCar">
      Delete
    </button>
  </div>
</template>

<script>
import { useRoute, useRouter } from 'vue-router'
import { AppState } from '../AppState'
import { reactive, computed, onMounted } from 'vue'
import { carsService } from '../services/CarsService'

export default {
  name: 'CarDetails',
  setup() {
    // ROUTE is the current page info
    const route = useRoute()
    // ROUTER is the toolset of changing routes automatically
    const router = useRouter()
    const state = reactive({
      car: computed(() => AppState.activeCar)
    })

    onMounted(async() => {
      try {
        await carsService.getCarById(route.params.id)
      } catch (error) {
        console.error(error)
      }
    })

    return {
      route,
      state,
      async deleteCar() {
        try {
          await carsService.deleteCar(state.car.id)
          // Router is a toolset, here used to change the page after the delete is completed
          // returning the user to the cars page
          AppState.activeCar = null
          router.push({ name: 'Cars' })
        } catch (error) {
          console.error(error)
        }
      }
    }
  },
  components: {}
}
</script>

<style lang="scss" scoped>

</style>
