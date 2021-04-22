<template>
  <div class="houses container">
    <div class="row">
      <div class="col py-3">
        <h2>Houses</h2>
        <button title="Open Create House Form"
                type="button"
                class="btn btn-outline-success"
                data-toggle="modal"
                data-target="#new-house-form"
        >
          <i class="fas fa-plus" aria-hidden="true"></i>
        </button>
      </div>
    </div>
    <div class="row">
      <!-- cars go here v-for car in cars -->
      <div v-if="state.loading">
        <i class="fas fa-spinner fa-spin"></i>
      </div>
      <House v-else v-for="house in state.houses" :key="house.id" :house="house" />
    </div>
  </div>
</template>

<script>
import { computed, onMounted, reactive } from 'vue'
import House from '../components/HouseComponent'
import { housesService } from '../services/HousesService'
import { AppState } from '../AppState'

export default {
  name: 'HousesPage',
  setup() {
    const state = reactive({
      loading: true,
      houses: computed(() => AppState.houses)
    })
    onMounted(async() => {
      try {
        await housesService.getHouses()
        state.loading = false
      } catch (error) {
        console.error(error)
      }
    })
    return {
      state
    }
  },
  components: {
    House
  }
}

</script>

<style lang="scss" scoped>
</style>
