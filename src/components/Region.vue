<template>
	<div>
		<div class="wrapper">
			<h1 class="title">Region Forecast</h1>
			<div class="sub-title">Updates every 24-hrs</div>
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
			icon: ''
		}
	},
	watch: {
		selected: function(val) {
			var regionForecast = Object.values(this.regionsForecast)[val].toLowerCase();

			if (regionForecast.includes('thunder')) {
				this.icon = 'fas fa-bolt';
			} else if (regionForecast.includes('showers')) {
				this.icon = 'fas fa-cloud-showers-heavy';
			} else if (regionForecast.includes('rain')) {
				if (regionForecast.includes('light')) {
					this.icon = 'fas fa-cloud-sun-rain';
				} else {
					this.icon = 'fas fa-cloud-showers-heavy';
				}
			} else if (regionForecast.includes('cloudy')) {
				this.icon = 'fas fa-cloud';
			} else if (regionForecast.includes('fair')) {
				if (regionForecast.includes('night')) {
					this.icon = 'fas fa-cloud-moon';
				} else {
					this.icon = 'fas fa-cloud-sun';
				}
			} else if (regionForecast.includes('windy')) {
				this.icon = 'fas fa-wind';
			}
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