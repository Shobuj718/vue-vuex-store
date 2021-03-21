<template>
    <div id="app">
    
        <navbar @search="search"></navbar>

        <div class="container">
            <div class="row">
                <div class="col-sm-9">
            
                    <inventory @newItemAdded="addCartItem" :items="items"></inventory>

                </div>

                <div class="col-sm-3">                    
                    <cart @itemRemove="removeItem" :items="cart"></cart>
                </div>

            </div>

        </div>
    </div>
</template>

<script>

import Navbar from './components/Navbar'
import Inventory from './components/Inventory'
import Cart from './components/Cart'
import data from './data.js'

export default {
    
    components: {
        Navbar,
        Inventory,
        Cart
    },

    data() {
        return {
            items: [],
            cart: []
        }
    },

    mounted() {
        console.log(data)
        this.items = data
    },
    methods: {
        search(keyword){
            console.log(keyword)
            this.items = data.filter(item => {
                return item.title.toLowerCase().indexOf(keyword.toLowerCase()) !== -1
            })
        },

        addCartItem(item) {
            this.cart.push(item) 
        },

        removeItem(index){
            this.cart.splice(index, 1)
        }

    }
}
</script>

<style>
  .container{
    padding-top: 10px;
  }
  .card{
    margin:2px;
  }
</style>
