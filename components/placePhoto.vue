<template>
  <div class="item" v-if="refPhoto">
    <img :src="img" class="rounded float-start" alt="restaurant" />
  </div>
  <div class="item" v-else>
    <div class="no-image pt-3">
      <p>No Image</p>
      Available
    </div>
  </div>
</template>

<script>
export default {
  props: {
    refPhoto: {
      type: String,
    },
  },
  data() {
    return {
      img: null,
    };
  },
  // fetch data from api
  mounted() {
    this.getPlacesPhoto();
  },
  updated() {
    this.getPlacesPhoto();
  },

  methods: {
    getPlacesPhoto() {
      this.isLoading = true;
      fetch(`http://localhost:9000/maps/getPlacesPhoto?ref=${this.refPhoto}`)
        .then((response) => response.json())
        .then((data) => {
          this.img = data;
          this.isLoading = false;
        });
    },
  },
};
</script>

<style lang="scss" scoped>
.item {
  width: 150px;
  object-fit: cover;
}
img {
  width: 150px;
  height: 100px;
  display: block; /* remove extra space below image */
}
.no-image {
  background-color: rgb(227, 227, 227);
  width: 150px;
  height: 100px;
  border-radius: 0.375rem;
  text-align: center;
}
</style>
