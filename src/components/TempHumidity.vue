<template>
	<div class="tempHumidity">
		<div class="stats">
			Temperature<br>
			{{ temperature.low }} - {{ temperature.high }}&#8451;
		</div> 
		<div class="stats">
			Humidity<br>
			{{ relativeHumidity.low }} - {{ relativeHumidity.high }} % <i class="fas fa-tint"></i>
		</div>
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
		font-size: 1.5em;
	}

	.stats {
		background-color: transparent;
		padding: 5%;
		transition: 0.3s ease-in-out;
	}

	

	@media only screen and (min-width: 768px) {

		.stats:hover {
			background-color: black;
			transform: translate(5%);
		}
	}

	@media only screen and (max-width: 768px) {

		.tempHumidity {
			display: flex;
			justify-content: center;
			align-items: center;
		}
	}

</style>