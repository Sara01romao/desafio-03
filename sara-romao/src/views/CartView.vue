<template>
  <div class="container">
    <h1 class="title">My Cart</h1>

    <main>
      <Message :msg="msg" v-show="msg" />
      <table v-if="cart.length !== 0">
        <tr>
          <th>Product</th>
          <th>Price</th>
          <th>Qty</th>
          <th>SubTotal</th>
          <th></th>
        </tr>

        <tr v-for="item in cart" :key="item.id">
          <td class="titleProduct">
            <router-link to="/">
              <img :src="item.image" :alt="item.title" />
              {{ item.title }}
            </router-link>
          </td>
          <td class="price">$ {{ item.price.toFixed(2) }}</td>
          <td class="qtyCount">
            <div>
              <button @click="removeQty(item.id)">-</button>
              {{ item.qtd }}
              <button @click="addQty(item.id)">+</button>
            </div>
          </td>
          <td class="price">${{ item.totalItem.toFixed(2) }}</td>

          <td class="remove" @click="removeProduct(item.id)">
            <img src="/assets/trash.svg" alt="Remove" />
          </td>
        </tr>
      </table>

      <div class="noProducts" v-else>
        <img src="/assets/cart-green.svg" alt="Cart" />
        <p>Your Cart is Empty</p>
        <router-link to="/">+ Add item</router-link>
      </div>
    </main>
    <div class="infoCart">
      <div>
        <h4>Total:</h4>
        <p>$ {{ $store.getters.total.toFixed(2) }}</p>
      </div>
      <button>Proceed To Checkout</button>
    </div>
  </div>
</template>


<script>
import { mapGetters } from "vuex";
import Message from '../components/Message.vue'
export default {
  components: {
    Message,
  },

  data() {
    return {
      
      msg:null
    };
  },
  computed: {
    ...mapGetters({
      cart: "getCart",
    }),
  },
  methods: {
    addQty(product) {
      this.$store.commit("incrementProduct", product);
    },

    removeQty(product) {
      this.$store.commit("decrementProduct", product);
    },

    removeProduct(product) {
      this.$store.commit("removeCart", product);
      this.msg= "Product was removed from cart"
      setTimeout(() => this.msg ="", 1500)
    },

   
  },
};
</script>


<style scoped>
.container {
  max-width: 900px;
  margin: 0 auto;
}

.title {
  text-align: center;
  margin-top: 20px;
}

main {
  overflow: auto;
  min-height: 70vh;
}

.noProducts {
  height: 50vh;
  display: flex;
  margin-top: 50px;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.noProducts p {
  font-size: 1.3rem;
  font-weight: bold;
  color: #616161;
}

.noProducts a {
  border: 2px solid #50e08c;
  border-radius: 5px;
  color: #0eaa4f;
  font-weight: bold;
  text-decoration: none;
  height: 35px;
  width: 120px;
  margin-top: 10px;
  display: flex;
  align-items: center;
  justify-content: center;
}

.noProducts a:hover {
  background: #d2f8e2;
}

table {
  font-family: arial, sans-serif;
  border-collapse: collapse;
  width: 100%;
  min-width: 500px;
  margin-top: 20px;
}

td,
th {
  border: 1px solid #dddddd;
  text-align: left;
  padding: 8px;
}

th {
  color: #616161;
}

tr:nth-child(even) {
  background-color: #f8f8f8;
}

td {
  text-align: center;
}

td:first-child {
  text-align: left;
}

.titleProduct a {
  display: flex;
  align-items: center;
  gap: 10px;
  max-width: 100%;
  text-decoration: none;
  color: #616161;
}

.titleProduct a:hover {
  color: #000;
}

.titleProduct img {
  width: 50px;
  height: 50px;
  object-fit: contain;
}

.price {
  width: 100px;
}

button {
  margin: auto 0px auto auto;
  height: 35px;
  background: #75e8a4;
  border: none;
  border-radius: 5px;
  font-weight: bold;
  padding: 10px 10px;
  cursor: pointer;
}

button:hover {
  background: #50e08c;
}

.qtyCount div {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 10px;
}

.qtyCount button{
  margin: 0px;
}

.infoCart {
  display: flex;
  flex-direction: column;
}



.infoCart button {
  margin-top: 10px;
  height: 40px;
}

.infoCart div {
  border: 1px solid rgb(223, 223, 223);
  display: flex;
  justify-content: flex-end;
  align-items: center;
  gap: 10px;
  padding: 0px 15px;
  height: 40px;
}

.remove img {
  cursor: pointer;
  opacity: 0.8;
  transition: 0.3s;
}

.remove img:hover {
  fill: red;
  opacity: 1;
}
</style>