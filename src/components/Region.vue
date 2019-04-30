<template>
	<div>
		<div class="wrapper">
			<div class="title">Region Forecast</div>
			<div v-if="selected">
				<div class="forecast">{{ region }}</div>
				<div class="weatherIcon">
					<i :class="icon"></i>
				</div>
			</div>
			<div v-else>
				<div class="forecast">Choose Region</div>
				<div class="weatherIcon">
					<i class="fas fa-sort-down"></i>
				</div>
			</div>
		</div>
		<div class="dropdown">
			<select class="select" v-model="selected">
				<option disabled value="">Select...</option>
				<option value="0">West</option> <!-- the values are numbers because i use them as indexes to access the values from the regionWeather obj i created in region() -->
				<option value="1">East</option>
				<option value="2">Central</option>
				<option value="3">South</option>
				<option value="4">North</option>
			</select>
		</div>
	</div>
</template>

<script>
//import { DateTime } from 'luxon';
export default {
	name: 'Region',
	components: {

	},
	props: ['regionsForecast', 'iconNames'],
	data() {
		return {
			selected: '',
			icon: '',
			backgroundImg: ''
		}
	},
	watch: {
		selected: function(val) {
			var regionForecast = Object.values(this.regionsForecast)[val].toLowerCase();

			if (regionForecast.includes('thunder')) {
				this.icon = 'fas fa-bolt';
				this.backgroundImg = 'thundery.jpg';
			} else if (regionForecast.includes('showers')) {
				this.icon = 'fas fa-cloud-showers-heavy';
				this.backgroundImg = 'showers.jpg';
			} else if (regionForecast.includes('rain')) {
				if (regionForecast.includes('light')) {
					this.icon = 'fas fa-cloud-sun-rain';
					this.backgroundImg = 'showers.jpg';
				} else {
					this.icon = 'fas fa-cloud-showers-heavy';
					this.backgroundImg = 'showers.jpg';
				}
			} else if (regionForecast.includes('cloudy')) {
				this.icon = 'fas fa-cloud';
				this.backgroundImg = 'cloudy.jpg';
			} else if (regionForecast.includes('fair')) {
				if (regionForecast.includes('night')) {
					this.icon = 'fas fa-cloud-moon';
					this.backgroundImg = 'fairNight.jpg';
				} else {
					this.icon = 'fas fa-cloud-sun';
					this.backgroundImg = 'fair.jpg';
				}
			} else if (regionForecast.includes('windy')) {
				this.icon = 'fas fa-wind';
				this.backgroundImg = 'windy.jpg'
			}
			this.$emit('add-region-weather', this.backgroundImg);
		}
	},
	computed: {
		region() {
			/*var startTime = this.weather.items[0].periods[0].time.start;
			var endTime = this.weather.items[0].periods[0].time.end;
			var interval = Interval.fromDateTimes(startTime, endTime);*/
			var regionForecast = Object.values(this.regionsForecast);
			//console.log(regionForecast)
			return regionForecast[this.selected];
		}
	}
}	
</script>

<style scoped>

</style>