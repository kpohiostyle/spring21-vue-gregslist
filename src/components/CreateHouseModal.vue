<template lang="">
  <div class="modal fade"
       id="new-house-form"
       tabindex="-1"
       role="dialog"
       aria-labelledby="exampleModalLabel"
       aria-hidden="true"
  >
    <div class="modal-dialog" role="document">
      <div class="modal-content">
        <div class="modal-header">
          <h5 class="modal-title" id="exampleModalLabel">
            New House
          </h5>
          <button type="button" class="close" data-dismiss="modal" aria-label="Close">
            <span aria-hidden="true">&times;</span>
          </button>
        </div>
        <form @submit.prevent="createHouse">
          <div class="modal-body">
            <div class="form-group">
              <label for="bedrooms">Bedrooms</label>
              <input type="text"
                     class="form-control"
                     id="bedrooms"
                     placeholder="Bedrooms..."
                     v-model="state.newHouse.bedrooms"
                     required
              >
            </div>
            <div class="form-group">
              <label for="bathrooms">Bathrooms</label>
              <input type="text"
                     class="form-control"
                     id="bathrooms"
                     placeholder="bathrooms..."
                     v-model="state.newHouse.bathrooms"
                     required
              >
            </div>
            <div class="form-group">
              <label for="levels">Levels</label>
              <input type="number"
                     class="form-control"
                     id="levels"
                     placeholder="Levels..."
                     min="1920"
                     max="2021"
                     v-model="state.newHouse.levels"
                     required
              >
            </div>
            <div class="form-group">
              <label for="price">Price</label>
              <input type="number"
                     class="form-control"
                     id="price"
                     placeholder="Price..."
                     min="1"
                     v-model="state.newHouse.price"
              >
            </div>
            <div class="form-group">
              <label for="description">Description</label>
              <input type="text"
                     class="form-control"
                     id="description"
                     placeholder="Description..."
                     minlength="3"
                     maxlength="20"
                     v-model="state.newHouse.description"
              >
            </div>
            <div class="form-group">
              <label for="imgUrl">Image Url</label>
              <input type="text" class="form-control" id="imgUrl" placeholder="Url..." v-model="state.newHouse.imgUrl">
            </div>
          </div>
          <div class="modal-footer">
            <button type="button" class="btn btn-secondary" data-dismiss="modal">
              Close
            </button>
            <button type="submit" class="btn btn-primary">
              Create
            </button>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
export default {

}
</script>
<style lang="">

</style>
