//bg-[#f7e9dc] style="background-color: #f7e9dc; z-index: -1"
<template>
<div
		class="background absolute h-screen w-screen bg-[#f7e9dc] -z-10"
></div>
<div class="container w-[380px] h-fit m-auto flex-col">
	<div class="header flex justify-between bg-[#ec755d] h-24 rounded-xl p-5 mb-5 items-center">
		<div class="header__content flex flex-col justify-between">
			<div class="header__content__title text-sm text-white">
				My balance
			</div>
			<div class="header__content__balance text-2xl text-white">
				${{ 500.28 }}
			</div>
		</div>
		<div class="header__toggle h-10">
			<svg class="max-w-full max-h-full" width="72" height="48" viewBox="0 0 72 48" xmlns="http://www.w3.org/2000/svg"><g fill="none" fill-rule="evenodd"><circle class="light-toggle" fill="#382314" cx="48" cy="24" r="24"/><circle class="dark-toggle" stroke="#FFF" stroke-width="2" cx="24" cy="24" r="23"/></g></svg>
		</div>
	</div>
	<div class="content min-h-fit max-h- flex-col justify-between py-7 px-5 bg-[#fffcf7] rounded-xl">
		<header class="content__header mb-5 text-2xl font-semibold">
			Spending - Last 7 days
		</header>
		<div class="content__graph flex justify-between">
			<div v-for="day in days" :key="day.id" class="content__graph__item flex flex-col h-[150px] w-[11%] text-center justify-end items-center">
				<div class="value mb-3 w-11 py-1 bg-[#382414] text-white rounded-sm text-[10px] font-semibold">${{ day.amount}}</div>
				<div class="graph-value w-full mb-1 cursor-pointer bg-[#ec755d] hover:bg-[#ff9b87] rounded-md"
						 :style="{ height: `${day.heightBar}px`}"
						 :class="{'max-value': day.day === maxDay.day}"
				></div>
				<div class="name text-sm opacity-30">{{ day.day }}</div>
			</div>
		</div>
		<hr class="my-5">
		<div class="content__footer flex justify-between">
			<div class="content__footer__left">
				<header class="content__footer__left__header text-sm opacity-30">
					Total this month
				</header>
				<div class="content__footer__left__value text-3xl font-semibold">
					${{ total }}
				</div>
			</div>
			<div class="content__footer__right flex flex-col justify-end">
					<div class="content__footer__right__value text-right font-semibold">
						{{2.4}}%
					</div>
					<div class="content__footer__right__sign text-sm opacity-30">
						from last month
					</div>
			</div>
		</div>
	</div>
</div>
	<div class="design">
		<img src="/expenses-chart-component-main/design/active-states.jpg" alt="design">
	</div>
</template>
<script>
export default {
	name: 'App',
	mounted(){
		this.dataHandler()
	},
	data(){
		return {
			days: [
				{
					"day": "mon",
					"amount": 17.45,
				},
				{
					"day": "tue",
					"amount": 34.91,
				},
				{
					"day": "wed",
					"amount": 52.36
				},
				{
					"day": "thu",
					"amount": 31.07
				},
				{
					"day": "fri",
					"amount": 23.39
				},
				{
					"day": "sat",
					"amount": 43.28
				},
				{
					"day": "sun",
					"amount": 25.48
				}
			]
		}
	},
	computed: {
		maxValue(){
			return Math.max(...this.days.map(day => day.amount))
		},
		total(){
			return this.days.reduce((sum, el) => sum + el.amount, 0)
		},
		maxDay(){
			return this.days.find(day => day.amount === this.maxValue)
		}
	},
	methods: {
		dataHandler(){
			this.days.forEach(day => {
				Object.assign(day, {
					'heightBar': this.heightHandler(day.amount)
				})
			})
		},
		heightHandler(value){
			return value * 100 / this.maxValue
		}
	}
}

</script>
<style>
.max-value:hover {
	background-color: #b4dfe4;
}

</style>
