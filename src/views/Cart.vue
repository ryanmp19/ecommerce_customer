<template>
<div class="container pt-5">
  <div class="card shopping-cart">
    <cart-header @saveCart="saveCart"></cart-header>
    <div class="card-body">
      <cart-body v-for="cart in carts" :key="cart.id" ref="cartBody[cart.id]" :cart="cart"></cart-body>
    </div>
    <cart-footer></cart-footer>
  </div>
</div>
</template>

<script>
import CartHeader from '../components/Cart/CartHeader'
import CartBody from '../components/Cart/CartBody'
import CartFooter from '../components/Cart/CartFooter'
import { mapState } from 'vuex'

export default {
  name: 'Cart',
  components: {
    CartHeader,
    CartBody,
    CartFooter
  },
  computed: {
    ...mapState(['carts'])
  },
  methods: {
    saveCart () {
      this.$refs.cartBody.saveCart()
    }
  },
  created () {
    this.$store.dispatch('fetchCartItems')
  }
}
</script>

<style>
.quantity {
  float: left;
  margin-right: 15px;
  background-color: #eee;
  position: relative;
  width: 80px;
  overflow: hidden
}

.quantity input {
  margin: 0;
  text-align: center;
  width: 15px;
  height: 15px;
  padding: 0;
  float: right;
  color: #000;
  font-size: 20px;
  border: 0;
  outline: 0;
  background-color: #F6F6F6
}

.quantity input.qty {
  position: relative;
  border: 0;
  width: 100%;
  height: 40px;
  padding: 10px 25px 10px 10px;
  text-align: center;
  font-weight: 400;
  font-size: 15px;
  border-radius: 0;
  background-clip: padding-box
}

.quantity .minus, .quantity .plus {
  line-height: 0;
  background-clip: padding-box;
  -webkit-border-radius: 0;
  -moz-border-radius: 0;
  border-radius: 0;
  -webkit-background-size: 6px 30px;
  -moz-background-size: 6px 30px;
  color: #bbb;
  font-size: 20px;
  position: absolute;
  height: 50%;
  border: 0;
  right: 0;
  padding: 0;
  width: 25px;
  z-index: 3
}

.quantity .minus:hover, .quantity .plus:hover {
  background-color: #dad8da
}

.quantity .minus {
  bottom: 0
}
.shopping-cart {
  margin-top: 20px;
}

/* Chrome, Safari, Edge, Opera */
input::-webkit-outer-spin-button,
input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* Firefox */
input[type=number] {
  -moz-appearance: textfield;
}
</style>
