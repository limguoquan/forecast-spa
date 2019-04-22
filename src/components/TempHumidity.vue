<template>
	<div class="row">
		<div class="col-2"></div> 
		<div class="forecast col-3">{{ temperature.low }} - {{ temperature.high }}&#8451;</div> 
		<div class="forecast col-3">{{ relativeHumidity.low }} - {{ relativeHumidity.high }} % <i class="fas fa-tint"></i></div>
		<div class="col-4"></div>
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
	
	.forecast {
		font-size: 3em;
		padding-bottom: 2%;
	}

</style>