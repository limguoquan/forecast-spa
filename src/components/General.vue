<template>
	<div class="wrapper">
		<h1 class="title">General Forecast</h1>
		<div class="sub-title">Updates every 24-hrs</div>
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
			icon: ''
		}
	},
	created() {
		if (this.generalForecast.toLowerCase().includes('thunder')) {
				this.icon = 'fas fa-bolt';
		} else if (this.generalForecast.toLowerCase().includes('showers')) {
			this.icon = 'fas fa-cloud-showers-heavy';
		} else if (this.generalForecast.toLowerCase().includes('rain')) {
			if (this.generalForecast.toLowerCase().includes('light')) {
				this.icon = 'fas fa-cloud-sun-rain';
			} else {
				this.icon = 'fas fa-cloud-showers-heavy';
			}
		} else if (this.generalForecast.toLowerCase().includes('cloudy')) {
			this.icon = 'fas fa-cloud';
		} else if (this.generalForecast.toLowerCase().includes('fair')) {
			if (this.generalForecast.toLowerCase().includes('night')) {
				this.icon = 'fas fa-cloud-moon';
			} else {
				this.icon = 'fas fa-cloud-sun';
			}
		} else if (this.generalForecast.toLowerCase().includes('windy')) {
			this.icon = 'fas fa-wind';
		}
	}
}	
</script>

<style scoped>
	

</style>