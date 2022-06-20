<template>
  <div>
      <h2>Damenmode</h2>
      <table style="margin-left:auto; margin-right: auto; text-align: left; ">
        <thead>
        <tr>
          <th >Artikel</th>
          <td>&nbsp;&nbsp;&nbsp;</td>
          <th>Preis</th>
          <th>&nbsp;</th>
        </tr>
        </thead>
        <tbody style="height: 200px">
        <tr v-for="(product, idx) in products" :key="idx">
          <td>{{ product.name }}</td>
          <td>&nbsp;&nbsp;&nbsp;</td>
          <td>{{ product.price.toFixed(2) }} CHF</td>
          <td>&nbsp;&nbsp;&nbsp;</td>
          <td>
            <b-button variant="success"  @click="addToCart(product) " @click.once="toggle = !toggle" style="color: #222d34; background-color:#9cff8e; border-color: #9cff8e; margin-right: 10px; padding: 3px 8px 3px 8px">+</b-button>
            <b-button v-show='toggle'  variant="danger" @click="removeFromCart(product)" style="color: #222d34; background-color:#cb5f5f; border-color: #cb5f5f; margin-right: 10px; padding: 3px 8px 3px 8px">-</b-button>
          </td>
        </tr>
        </tbody>
      </table>
  </div>
</template>

<script>
import { mapState } from 'vuex';
export default {
  name: 'Products',
  computed: mapState(['products']),
  data() {
    return {
      toggle: false
    }
  },
  methods: {
    addToCart(product) {
      this.$store.commit('addToCart', product);
    },
    removeFromCart(product) {
      this.$store.commit('removeFromCart', product);
    }
  },
  created() {
    this.$store.dispatch("loadProducts")
  },

}



</script>

