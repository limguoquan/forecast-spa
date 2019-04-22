<template>
	<div class="row">
		<div class="col-2"></div>
		<div class="col-3">
			<h1 class="title">Future Forecasts</h1>
			<div class="wrapper" v-for="forecast in fourDayForecast">
				<div class="date">{{ dayOfWeek(forecast) }}<br>{{ forecast.date }}</div>
				<div class="temp-forecast">{{ forecast.temperature.low }} - {{ forecast.temperature.high }}&#8451;
					<br>{{ forecast.forecast.substring(0, forecast.forecast.length-1) }} 
				</div> <!-- to remove the full stop at the end -->
			</div>
		</div>
		<div class="col-7"></div>
	</div>
</template>

<script>
import { DateTime } from 'luxon';

export default {
	name: 'FourDayForecast',
	props: ['fourDayForecast'],
	components: {

	},
	computed: {

	},
	data() {
		return {
			// futureDates: []
		}
	},
	methods: {
		dayOfWeek(forecast) {
			return DateTime.fromISO(forecast.date).weekdayLong;
		}
	}
/*	created() {
		var tmr = DateTime.local().plus({ days: 1 }).endOf('day');
		var days = 0;

		for (var i = 0; i < 4; i++) {
			this.futureDates[i] = DateTime.fromISO(tmr.plus({ days: days++ }).startOf('day').toISO().substring(0, 19)).weekdayShort;
		}
	}*/
}
</script>

<style scoped>

	.wrapper {
		padding-bottom: 10%;
	}

	.date {
		font-weight: bold;
		padding-bottom: 2%;
	}

	.temp-forecast {
		font-size: 1.2em;
	}

</style>