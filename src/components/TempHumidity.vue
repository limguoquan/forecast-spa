<template>
	<div class="tempHumidity">
		<div class="temp">{{ temperature.low }} - {{ temperature.high }}&#8451;</div> 
		<div class="humidity">{{ relativeHumidity.low }} - {{ relativeHumidity.high }} % <i class="fas fa-tint"></i></div>
	</div>
</template>

<script>
export default {
	name: 'TempHumidity',
	props: ['temperature', 'relativeHumidity'],
	components: {

	},
	computed: {

	},
	data() {
		return {

		}
	}
}	
</script>

<style scoped>
	
	.tempHumidity {
		text-orientation: sideways;
	}


</style>