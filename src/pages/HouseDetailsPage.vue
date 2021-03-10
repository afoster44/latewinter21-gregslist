<template>
  <div class="house-details container-fluid">
    <div class="row">
      <div class="card col-4">
        <img class="card-img-top" :src="state.house.imgUrl" alt="">
        <div class="card-body">
        <h4 class="card-title">Bedrooms: {{state.house.bedrooms}} - Bathrooms: {{state.house.bathrooms}} </h4>
        <p class="card-text">Price: {{state.house.price}}</p>
        <p class="card-text">Stories: {{state.house.levels}}</p>
        <p class="card-text">{{state.house.description}}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import { reactive, onMounted } from 'vue'

import { computed } from '@vue/runtime-core'
import { AppState } from '../Appstate'
import { housesService } from '../services/HousesService'
import { useRoute } from 'vue-router'
export default {
  name: 'HouseDetailsPage',
  setup() {
    const route = useRoute()
    const state = reactive({
      house: computed(() => AppState.activeHouse)
    })
    onMounted(() => {
      housesService.getHouse(route.params.id)
    })
    return {
      state,
      route
    }
  },
  components: {}
}
</script>

<style lang="scss" scoped>

</style>
