<template>
  <div class="productCart">
    <router-link to="/">
      <img :src="product.image" :alt="product.title" class="productImg" />
      <p class="productTitle">{{ product.title }}</p>
      <h3>${{ product.price.toFixed(2) }}</h3>
      <small v-if="product.rating.rate == 5">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
      </small>
      <small v-else-if="product.rating.rate >= 4.5 && product.rating.rate < 5">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYG.svg" alt="start" />
      </small>
      <small v-else-if="product.rating.rate >= 4 && product.rating.rate < 4.5">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>
      <small v-else-if="product.rating.rate >= 3 && product.rating.rate <= 3.4">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>

      <small v-else-if="product.rating.rate >= 3.5 && product.rating.rate < 4">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYG.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>
      <small v-else-if="product.rating.rate >= 2 && product.rating.rate <= 2.4">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>

      <small v-else-if="product.rating.rate >= 2.5 && product.rating.rate < 3">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYG.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>
      <small v-else-if="product.rating.rate >= 1 && product.rating.rate <= 1.4">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>

      <small v-else-if="product.rating.rate >= 1.5 && product.rating.rate < 2">
        <img src="/assets/starYellow.svg" alt="start" />
        <img src="/assets/starYG.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>
      <small v-else>
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
        <img src="/assets/starGrey.svg" alt="start" />
      </small>
      {{ product.rating.rate }}
    </router-link>
    <button
      @click="addCart(product.id, product.title, product.price, product.image)"
    >
      <div class="infoCart">
        <img src="/assets/cart-btn.svg" />
      </div>
      Add
    </button>
  </div>
</template>

<script>
export default {
  name: "Product",
  props: ["product"],

  data() {
    return {};
  },
  emits: ['show-msg'],

  methods: {
    addCart(id, title, price, image) {
      const product = {
        id: id,
        title: title,
        price: price,
        image: image,
      };

      this.$store.commit("addInCart", product);
      

      this.$emit('show-msg', "Your product has been added to cart")
    },
  },
};
</script>

<style scoped>
.productCart {
  max-width: 250px;
  border-radius: 10px;
  padding: 20px 10px;
  text-align: center;
}

.productCart a {
  text-decoration: none;
  color: rgb(49, 49, 49);
  transition: 0.3s;
}

.productCart a:hover {
  color: rgb(0, 0, 0);
}

.productImg {
  width: 100%;
  height: 250px;
  background: #fff;
  border: 1px solid rgb(240, 240, 240);
  object-fit: contain;
  padding: 10px 5px;
}

.productTitle {
  max-width: 60ch;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  padding: 0px 5px;
}
.productCart button {
  width: 100%;
  height: 35px;
  margin-top: 10px;
  background: #75e8a4;
  border: none;
  border-radius: 5px;
  display: flex;
  gap: 10px;
  justify-content: center;
  align-items: center;
  cursor: pointer;
  margin-bottom: 5px;
}

.productCart button:hover {
  background: #3de282;
}

.infoCart {
  display: flex;
  align-items: center;
  gap: 5px;
}

.productCart h3 {
  margin: 5px 0px 10px;
}
</style>