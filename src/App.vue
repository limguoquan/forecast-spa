<template>
	<div id="app">
		<TempHumidity :temperature="weather.items[0].general.temperature" :relativeHumidity="weather.items[0].general.relative_humidity"/>
		<div class="row">
			<div class="col-2"></div>
			<div class="col-3">
				<General :generalForecast="weather.items[0].general.forecast" :iconNames="iconNames" />
			</div>
			<div class="col-3">
				<Region :regionsForecast="weather.items[0].periods[0].regions" :iconNames="iconNames" />
			</div>
			<div class="col-3">
				<TwoHourForecast :twoHourForecast="twoHourForecast.items[0].forecasts" :iconNames="iconNames" />
			</div>
			<div class="col-1"></div>
		</div>
		<div class="row">
			<FourDayForecast :fourDayForecast="fourDayForecast.items[0].forecasts" />
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
			iconNames: ['fas fa-bolt', 'fas fa-cloud-showers-heavy', 'fas fa-cloud-sun-rain', 'fas fa-cloud-sun', 'fas fa-cloud-moon', 'fas fa-cloud', 'fas fa-wind']
		}
	},
	created() {
		var now = DateTime.local();
		//console.log(now.toString());
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
	}
}
</script>

<style>	

	* {
		box-sizing: border-box;
		padding: 0;
		margin: 0;
		font-family: 'Raleway', sans-serif;
	}

	/* For mobile phones: */
	[class*="col-"] {
		width: 100%;
		float: left;
		padding: 15px;
	}

	.row::after {
		content: "";
		clear: both;
		display: table;
	}

	@media only screen and (min-width: 768px) {
		/* For desktop: */
		.col-1 {width: 8.33%;}
		.col-2 {width: 16.66%;}
		.col-3 {width: 25%;}
		.col-4 {width: 33.33%;}
		.col-5 {width: 41.66%;}
		.col-6 {width: 50%;}
		.col-7 {width: 58.33%;}
		.col-8 {width: 66.66%;}
		.col-9 {width: 75%;}
		.col-10 {width: 83.33%;}
		.col-11 {width: 91.66%;}
		.col-12 {width: 100%;}
	}

	.overview {
		font-size: 2em;
		font-weight: bold;
		padding-top: 2%
	}

	.wrapper {
		display: flex;
		flex-direction: column;
		align-items: left;
		justify-content: center;
		border-left: 2px solid #5E5E5E;
		padding-left: 5%;
	}

	.title {
		padding-bottom: 5%;
	}

	.sub-title {
		font-size: 0.8em;
		padding-bottom: 5%;
	}

	.forecast {
		font-size: 1.5em;
		padding-bottom: 5%;
	}

	.weatherIcon {
		font-size: 5em;

	}

	.fas {
		color: #5E5E5E;
	}

	@media only screen and (max-width: 768px) {

		.overview, .wrapper, .forecast, .weatherIcon, .title {
			text-align: center;
		}

		.wrapper {
			border-left: none;
			padding-left: 0;
		}
	}
</style>
