<template>
  <div class="house-details" v-if="state.house">
    <div class="row">
      <div class="col-md-12">
        <div class="card shadow">
          <img class="card-img-top" :src="state.house.imgUrl" alt="">
          <div class="card-body">
            <h4 class="card-title">
              something else
            </h4>
            <p class="card-text">
              Bathrooms: {{ state.house.bathrooms }} | Bedrooms: {{ state.house.bedrooms }}
            </p>
          </div>
        </div>
      </div>
    </div>
    <button type="button" class="btn btn-danger" @click="deleteHouse">
      Delete
    </button>
  </div>
</template>

<script>
import { useRoute, useRouter } from 'vue-router'
import { AppState } from '../AppState'
import { reactive, computed, onMounted } from 'vue'
import { housesService } from '../services/HousesService'

export default {
  name: 'HouseDetails',
  setup() {
    const route = useRoute()
    const router = useRouter()
    const state = reactive({
      house: computed(() => AppState.activeHouse)
    })
    onMounted(async() => {
      try {
        await housesService.getHouseById(route.params.id)
      } catch (error) {
        console.error(error)
      }
    })
    return {
      route,
      state,
      async deleteHouse() {
        try {
          await housesService.deleteHouse(state.house.id)
          AppState.activeHouse = null
          router.push({ name: 'Houses' })
        } catch (error) {
          console.error(error)
        }
      }
    }
  },
  components: {
  }

}
</script>
<style lang="">

</style>
