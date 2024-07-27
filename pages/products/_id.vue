<template>
  <div v-if="rating.rate" class="container">
    <div class="container-left">
      <v-img :src="product.image"></v-img>
    </div>
    <div class="container-right">
      <h1>{{ product.title }}</h1>
      <p>{{ product.description }}</p>
      <div class="container-rating">
        <v-rating
          v-model="rating.rate"
          background-color="orange lighten-3"
          half-increments
          color="orange"
          readonly
        ></v-rating>
        <v-chip class="ma-2">
          {{ rating.count }}
        </v-chip>
      </div>
      <div class="container-button">
        <v-btn color="orange" class="ma-2 white--text">
          <v-icon left dark> mdi-plus </v-icon>
          Add To Cart
        </v-btn>
      </div>
    </div>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  name: 'ProductPage',
  data() {
    return {
      product: {},
      rating: {},
    }
  },
  head() {
    return { title: this.product.title }
  },
  mounted() {
    axios
      .get('https://fakestoreapi.com/products/' + this.$route.params.id)
      .then((response) => (this.product = response.data))
      .then((data) => (this.rating = data.rating))
  },
}
</script>
<style lang="scss" scoped>
.container {
  display: flex;
  align-items: center;
  &-left {
    margin: 20px;
    div.v-image {
      max-width: 250px;
      border-radius: 5%;
    }
  }
  &-right {
    margin: 20px;
  }
  &-rating {
    display: flex;
    align-items: center;
  }
}

@media screen and (max-width: 639px) {
  .container {
    flex-wrap: wrap;
    justify-content: center;
    &-button {
      text-align: center;
    }
  }
}
</style>
