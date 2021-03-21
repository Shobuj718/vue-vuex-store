<template>

	<div v-if="item" class="row">
		<div class="col-sm-6">
			<img :src="item.photo" alt="photo">
		</div>
		<div class="col-sm-6">
			<h2>{{ item.title }}</h2>
			<p>{{ item.description }}</p>

			<div class="card-footer">
				<span>${{ item.price }}</span>
				<button @click="addToCart(item)" class="btn btn-sm btn-primary float-right"> + Add</button>
			</div>

		</div>
	</div>
	<h2 v-else="item">Loading</h2>
</template>

<script>
	import axios from 'axios'
	export default {
		data() {
			return {
				item: null
			}
		},
		mounted() {
			this.fetchItem()
		},
		methods: {
			fetchItem() {
				var self = this
				axios.get('http://localhost:3000/item/'+this.$route.params.id).then( res => {
					self.item = res.data
					console.log(res.data)
				})
			},
			addToCart(item) {
				//this.$store.commit('addToCart', item)
				this.$store.dispatch('addToCart', item)
			}
		}
	}
</script>


<style>
</style>