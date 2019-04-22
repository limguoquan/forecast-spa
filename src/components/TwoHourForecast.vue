<template>
	<div>
		<div class="wrapper">
			<h1 class="title">Area Forecast</h1>
			<div class="sub-title">Updates every 2-hrs</div>
			<div v-if="areaForecast">
				<div class="forecast">{{ areaForecast }}</div>
				<div class="weatherIcon">
					<i :class="icon"></i>
				</div>
			</div>
			<div v-else>
				<div class="forecast">Choose Area</div>
				<div class="weatherIcon">
					<i class="fas fa-sort-down"></i>
				</div>
			</div>
		</div>
		<div class="dropdown">
			<select class="select" v-model="areaForecast">
				<option disabled value="">Select...</option>
				<option  v-for="forecast in twoHourForecast" :value="forecast.forecast">{{ forecast.area }}</option>
			</select>
		</div>
	</div>
</template>

<script>
export default {
	name: 'TwoHourForecast',
	props: ['twoHourForecast', 'iconNames'],
	components: {

	},
	computed: {

	},
	data() {
		return {
			areaForecast: '',
			icon: ''
		}
	},
	watch: {
		areaForecast: function(val) {
			if (val.toLowerCase().includes('thunder')) {
				this.icon = 'fas fa-bolt';
			} else if (val.toLowerCase().includes('showers')) {
				this.icon = 'fas fa-cloud-showers-heavy';
			} else if (val.toLowerCase().includes('rain')) {
				if (val.toLowerCase().includes('light')) {
					this.icon = 'fas fa-cloud-sun-rain';
				} else {
					this.icon = 'fas fa-cloud-showers-heavy';
				}
			} else if (val.toLowerCase().includes('cloudy')) {
				this.icon = 'fas fa-cloud';
			} else if (val.toLowerCase().includes('fair')) {
				if (val.toLowerCase().includes('night')) {
					this.icon = 'fas fa-cloud-moon';
				} else {
					this.icon = 'fas fa-cloud-sun';
				}
			} else if (val.toLowerCase().includes('windy')) {
				this.icon = 'fas fa-wind';
			}
		}
	}
}	
</script>

<style scoped>

.dropdown {
		display: flex;
		justify-content: flex-start;
		padding-top: 5%;
	}

	.select {
		font-size: 1em;
		cursor: pointer;
	}

	@media only screen and (max-width: 768px) {
		.dropdown {
			justify-content: center;
		}
	}

</style>