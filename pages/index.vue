<template>
  <div class="row mt-10">
    <div class="col-12">
      <div class="input-group input-group-lg">
        <input
          type="text"
          placeholder="Search..."
          class="form-control border rounded-md px-4 py-3 w-full text-lg focus:outline-gray-800"
          v-model="keyword"
          v-on:keyup.enter="getPlaces"
        />
        <button type="submit" class="btn border" @click="getPlaces">
          <font-awesome-icon :icon="['fas', 'magnifying-glass']" />
        </button>
      </div>
    </div>
    <hr class="mt-5" />
    <!-- result data list -->
    <loadingScreen v-show="isLoading" />
    <div v-for="list in mapDataLists?.data" :key="list.list">
      <!-- click to google map web site -->
      <a
        :href="
          'https://www.google.com/maps/search/?api=1&query=' +
          list.geometry.location.lat +
          '%2C' +
          list.geometry.location.lng +
          '&query_place_id=' +
          list.place_id
        "
        target="_blank"
        rel="noreferrer"
        class="list-group-item list-group-item-action card-hover p-2"
      >
        <div class="row">
          <div class="col-md-10 col-6">
            <h4>{{ list.name }}</h4>
            <p>
              <starRating :value="list.rating" />
              (
              {{ list.user_ratings_total ? list.user_ratings_total : 0 }}
              )
            </p>
            <span>{{ list.vicinity }}</span>
          </div>
          <div class="col-md-1 col-1">
            <placePhoto
              :refPhoto="list.photos ? list.photos[0]?.photo_reference : null"
            />
          </div>
        </div>
      </a>
      <hr />
    </div>
    <!-- show no data result-->
    <div v-show="mapDataLists?.data.length === 0">
      <h1>No Result..</h1>
    </div>
  </div>
</template>

<script>
import starRating from "../components/starRating.vue";
import placePhoto from "../components/placePhoto.vue";
import loadingScreen from "../components/loadingScreen.vue";
export default {
  data() {
    return {
      mapDataLists: null,
      keyword: "",
      isLoading: false,
    };
  },
  // fetch data from api
  async mounted() {
    this.getPlaces();
  },
  methods: {
    getPlaces() {
      this.isLoading = true;
      fetch(
        `http://localhost:9000/maps/getPlacesNearby?keyword=${this.keyword}`
      )
        .then((response) => response.json())
        .then((data) => {
          this.mapDataLists = data;
          this.isLoading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
hr {
  border: 1px solid #dee2e6;
}
.card-hover:hover {
  background-color: #e8e8e8;
}
</style>
