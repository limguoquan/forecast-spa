<template>
	<div class="wrapper">
		<div class="title">General Forecast</div>
		<div class="forecast">{{ generalForecast }}</div>
		<template v-for="name in iconNames">
			<div class="weatherIcon" v-if="icon === name">
				<i v-bind:class="icon"></i>
			</div>
		</template>
	</div>
</template>

<script>
export default {
	name: 'General',
	props: ['generalForecast', 'iconNames'],
	components: {

	},
	computed: {

	},
	data() {
		return {
			icon: '',
			backgroundImg: ''
		}
	},
	created() {

		if (this.generalForecast.toLowerCase().includes('thunder')) {
				this.icon = 'fas fa-bolt';
				this.backgroundImg = 'thundery.jpg';
		} else if (this.generalForecast.toLowerCase().includes('showers')) {
			this.icon = 'fas fa-cloud-showers-heavy';
			this.backgroundImg = 'showers.jpg';
		} else if (this.generalForecast.toLowerCase().includes('rain')) {
			if (this.generalForecast.toLowerCase().includes('light')) {
				this.icon = 'fas fa-cloud-sun-rain';
				this.backgroundImg = 'showers.jpg';
			} else {
				this.icon = 'fas fa-cloud-showers-heavy';
				this.backgroundImg = 'showers.jpg';
			}
		} else if (this.generalForecast.toLowerCase().includes('cloudy')) {
			this.icon = 'fas fa-cloud';
			this.backgroundImg = 'cloudy.jpg';
		} else if (this.generalForecast.toLowerCase().includes('fair')) {
			if (this.generalForecast.toLowerCase().includes('night')) {
				this.icon = 'fas fa-cloud-moon';
				this.backgroundImg = 'fairNight.jpg';
			} else {
				this.icon = 'fas fa-cloud-sun';
				this.backgroundImg = 'fair.jpg';
			}
		} else if (this.generalForecast.toLowerCase().includes('windy')) {
			this.icon = 'fas fa-wind';
			this.backgroundImg = 'cloudy.jpg';
		}
		this.$emit('add-general-weather', this.backgroundImg);
	}
}	
</script>

<style scoped>


</style>