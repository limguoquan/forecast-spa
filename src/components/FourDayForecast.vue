<template>
	<div class="wrapper">
		<div class="title">Future Forecasts</div>
		<div class="forecast" v-for="forecast in fourDayForecast">
			<div class="date">{{ dayOfWeek(forecast) }}<br>{{ forecast.date }}</div>
			<div class="temp-forecast">{{ forecast.temperature.low }} - {{ forecast.temperature.high }}&#8451;
				<br>{{ forecast.forecast.substring(0, forecast.forecast.length-1) }} 
			</div> <!-- to remove the full stop at the end -->
		</div>
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

	.forecast, .title {
		background-color: transparent;
		opacity: 0.7;
		transition: 0.3s ease-in-out;
	}

	.forecast:hover, .title:hover {
		opacity: 1;
		background-color: black;
	}

	@media only screen and (max-width: 768px) {
		.forecast, .title {
			opacity: 1;
		}
	}

</style>