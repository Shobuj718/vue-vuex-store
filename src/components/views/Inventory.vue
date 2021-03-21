<template>

	<div v-if="!loading" class="row">  

	    <div v-for="(item, index) in items" :key="index" class="card" style="width: 18rem;">

	    	<router-link :to="{ path: '/item/'+item.id }" tag="div">
		        <img :src="item.photo" class="card-img-top" alt="no image">
		        <div class="card-body">
		          <h5 class="card-title">{{ item.title }}</h5>
		        </div>
	        </router-link>

	        <div class="card-footer">
	    		<p class="card-text">{{ item.price }}</p>
	          	<a @click="addToCart(item)" class="btn btn-primary">+ Add Cart</a>
	    	</div>
	    </div>

    </div>

    <h2	v-else="loading">Loading...</h2>

</template>

<script>

	import axios from 'axios'

	export default {
		data(){
			return {
				loading: true,
				items: []
			}
		},
		mounted() {
			this.fetchInventory()
		},
		methods: {
			addToCart(item) {
				this.$emit('newItemAdded', item)
			},
			fetchInventory() {
				var self = this
				axios.get('http://localhost:3000/items').then(res => {
					setTimeout(function() {
						self.items = res.data
						self.loading = false
					}, 2000)

				})
			}
		}
		
	}
</script>

<style>

</style>