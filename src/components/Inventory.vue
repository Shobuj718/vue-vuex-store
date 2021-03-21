<template>

	<div class="row">  

	    <div v-for="(item, index) in items" :key="index" class="card" style="width: 18rem;">
	        <img :src="item.photo" class="card-img-top" alt="no image">
	        <div class="card-body">
	          <h5 class="card-title">{{ item.title }}</h5>
	          <p class="card-text">{{ item.price }}</p>
	          <a @click="addToCart(item)" class="btn btn-primary">+ Add Cart</a>
	        </div>
	    </div>

    </div>

</template>

<script>
	export default {
		props: ['items'],
		methods: {
			addToCart(item) {
				this.$emit('newItemAdded', item)
			}
		}
	}
</script>

<style>

</style>