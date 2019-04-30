<template>
	<div id="app">
		<div class="row upper-half">
			<div class="col-2">
				<TempHumidity :temperature="weather.items[0].general.temperature" :relativeHumidity="weather.items[0].general.relative_humidity"/>
			</div>
			<div class="col-5 item" :style="setGeneralImg">
				<General v-on:add-general-weather="addGeneralWeather" :generalForecast="weather.items[0].general.forecast" :iconNames="iconNames" />
			</div>
			<div class="col-5 item" :style="setRegionImg">
				<Region v-on:add-region-weather="addRegionWeather" :regionsForecast="weather.items[0].periods[0].regions" :iconNames="iconNames" />
			</div>
		</div>
		<div class="row lower-half">
			<div class="filler col-2"></div>
			<div class="col-5">
				<FourDayForecast :fourDayForecast="fourDayForecast.items[0].forecasts" />
			</div>
			<div class="col-5 item" :style="setAreaImg">
				<TwoHourForecast v-on:add-area-weather="addAreaWeather" :twoHourForecast="twoHourForecast.items[0].forecasts" :iconNames="iconNames" />
			</div>
		</div>		
	</div>
</template>

<script>
import { DateTime } from 'luxon';
import TempHumidity from './components/TempHumidity';
import General from './components/General';
import Region from './components/Region';
import FourDayForecast from './components/FourDayForecast';
import TwoHourForecast from './components/TwoHourForecast';

export default {
	name: 'app',
	components: {
		TempHumidity,
		General,
		Region,
		FourDayForecast,
		TwoHourForecast
	},
	data() {
		return {
			weather: [],
			fourDayForecast: [],
			twoHourForecast: [],
			iconNames: ['fas fa-bolt', 'fas fa-cloud-showers-heavy', 'fas fa-cloud-sun-rain', 'fas fa-cloud-sun', 'fas fa-cloud-moon', 'fas fa-cloud', 'fas fa-wind'],
			generalWeather: '',
			regionWeather: '',
			areaWeather: ''
		}
	},
	created() {
		var now = DateTime.local();
		var date = now.toISO().substring(0, 19);
		console.log(date);
		var url = 'https://api.data.gov.sg/v1/environment/24-hour-weather-forecast?date_time=' + date;
		var fourDayUrl = 'https://api.data.gov.sg/v1/environment/4-day-weather-forecast?date_time=' + date;
		var twoHourUrl = 'https://api.data.gov.sg/v1/environment/2-hour-weather-forecast?date_time=' + date;
		//console.log(url);
		fetch(url)
			.then(response => response.json())
			.then(data => this.weather = data)
			.catch(error => console.error(error))

		fetch(fourDayUrl)
			.then(response => response.json())
			.then(data => this.fourDayForecast = data)
			.catch(error => console.error(error))

		fetch(twoHourUrl)
			.then(response => response.json())
			.then(data => this.twoHourForecast = data)
			.catch(error => console.error(error))
	},
	methods: {
		addGeneralWeather(weather) {
			this.generalWeather = weather;
		},
		addRegionWeather(weather) {
			this.regionWeather = weather;
		},
		addAreaWeather(weather) {
			this.areaWeather = weather;
		},
		setBackgroundImg(weather) {
			switch(weather) {
				case 'thundery.jpg':
					return 'backgroundImage: ' + 'url(' + require('./assets/backgroundImg/thundery.jpg') + ')'
				case 'cloudy.jpg':
					return 'backgroundImage: ' + 'url(' + require('./assets/backgroundImg/cloudy.jpg') + ')'
				case 'fair.jpg':
					return 'backgroundImage: ' + 'url(' + require('./assets/backgroundImg/fair.jpg') + ')'
				case 'fairNight.jpg':
					return 'backgroundImage: ' + 'url(' + require('./assets/backgroundImg/fairNight.jpg') + ')'
				case 'showers.jpg':
					return 'backgroundImage: ' + 'url(' + require('./assets/backgroundImg/showers.jpg') + ')'
			}
		}
	},
	computed: {
		setGeneralImg() {
			return this.setBackgroundImg(this.generalWeather);
		},
		setRegionImg() {
			return this.setBackgroundImg(this.regionWeather);
		},
		setAreaImg() {
			return this.setBackgroundImg(this.areaWeather);
		}
	}
}
</script>

<style src="./assets/cssFiles/app.css">	

</style>
