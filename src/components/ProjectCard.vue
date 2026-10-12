<template>
	<!-- <div class="card-deck my-5 justify-content-center"> -->
		<div class="card col-md-3">
			<!-- : is a directive to bind the image to the src attribute -->
		    <img :src="project.image" class="card-img-top card-img" alt="...">
		    <div class="card-body">
			    <h5 class="card-title">{{ project.title }}</h5>
			    <p class="card-text">
			        {{ project.description }}
			    </p> 
		    </div>
		</div>
</template>

<script setup>
	// defineProps is a Composition API method. it will allows us to receive the data from a parent component.
	import { defineProps } from 'vue';

	// This will be used to define/describe the data that the component will receive
	defineProps({
		// Check the data type of the value
		project: Object
	})
</script>