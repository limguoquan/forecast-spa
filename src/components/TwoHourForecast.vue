<template>
	<div class="wrapper">
		<div class="title">Area Forecast</div>
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
			icon: '',
			backgroundImg: ''
		}
	},
	watch: {
		areaForecast: function(val) {
			if (val.toLowerCase().includes('thunder')) {
				this.icon = 'fas fa-bolt';
				this.backgroundImg = 'thundery.jpg';
			} else if (val.toLowerCase().includes('showers')) {
				this.icon = 'fas fa-cloud-showers-heavy';
				this.backgroundImg = 'showers.jpg';
			} else if (val.toLowerCase().includes('rain')) {
				if (val.toLowerCase().includes('light')) {
					this.icon = 'fas fa-cloud-sun-rain';
					this.backgroundImg = 'showers.jpg';
				} else {
					this.icon = 'fas fa-cloud-showers-heavy';
					this.backgroundImg = 'showers.jpg';
				}
			} else if (val.toLowerCase().includes('cloudy')) {
				this.icon = 'fas fa-cloud';
				this.backgroundImg = 'cloudy.jpg';
			} else if (val.toLowerCase().includes('fair')) {
				if (val.toLowerCase().includes('night')) {
					this.icon = 'fas fa-cloud-moon';
					this.backgroundImg = 'fairNight.jpg';
				} else {
					this.icon = 'fas fa-cloud-sun';
					this.backgroundImg = 'fair.jpg';
				}
			} else if (val.toLowerCase().includes('windy')) {
				this.icon = 'fas fa-wind';
				this.backgroundImg = 'cloudy.jpg';
			}
			this.$emit('add-area-weather', this.backgroundImg);
		}
	}
}	
</script>

<style scoped>


</style>