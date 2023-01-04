<template>
    
</template>


<script>
/* make axios get requestion /panier */
import { defineComponent, ref, onMounted, created } from 'vue'
import axios from 'axios'
export default {
    name: 'CartView',
    setup() {
        const cart = ref([])
        const shopitem = ref([])
        const getCart = async () => {
        const response = await axios.get('http://localhost:3000/panier')
        cart.value = response.data
        console.log(response.data)

        }
        onMounted(getCart)
        
        const getShop = async () => {
        const response = await axios.get('http://localhost:3000/shop')
        shopitem.value = response.data
        console.log(response.data)

        }
        onMounted(getShop)
        /* keep only item with id match between cart.panier and shopitem.id */
        const getOwnCart = async () => {
        const cartitem = shopitem.value.filter((item) => cart.value.panier.includes(item.id))
        console.log("cartitem")
        console.log(cartitem)
        }
        created(getOwnCart)
    },
  }
</script>
