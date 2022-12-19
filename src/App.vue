<template>
<div class="background absolute h-screen w-screen bg-[#f7e9dc] -z-10"/>
<div class="container w-[380px] h-fit mx-auto flex-col">
	<div class="header flex justify-between bg-[#ec755d] h-24 rounded-xl p-5 mb-5 items-center">
		<div class="header__content flex flex-col justify-between">
			<div class="header__content__title text-sm text-white">
				My balance
			</div>
			<div class="header__content__balance text-2xl text-white font-semibold">
				${{ userBalance }}
			</div>
		</div>
		<div class="header__toggle h-10">
			<svg class="max-w-full max-h-full" width="72" height="48" viewBox="0 0 72 48" xmlns="http://www.w3.org/2000/svg">
				<g fill="none" fill-rule="evenodd">
				<circle class="light-toggle" fill="#382314" cx="48" cy="24" r="24"/>
				<circle class="dark-toggle" stroke="#FFF" stroke-width="2" cx="24" cy="24" r="23"/>
				</g>
			</svg>
		</div>
	</div>
	<div class="content min-h-fit max-h- flex-col justify-between py-7 px-5 bg-[#fffcf7] rounded-xl">
		<header class="content__header mb-5 text-2xl font-semibold">
			Spending - Last 7 days
		</header>
		<div class="content__graph flex justify-between">
			<div v-for="day in days" :key="day.id"
					 class="content__graph__item flex flex-col h-[150px] w-[11%] text-center justify-end items-center">
				<div v-if="day.active"
						 class="value mb-3 w-11 py-1 bg-[#382414] text-white rounded-sm text-[10px] font-semibold">
					${{ day.amount}}
				</div>
				<div class="graph-value w-full mb-1 cursor-pointer bg-[#ec755d] hover:bg-[#ff9b87] rounded-md"
						 @mouseover="day.active = true"
						 @mouseleave="day.active = false"
						 :style="{ height: `${day.heightBar}px`}"
						 :class="{
							 'hover:bg-[#b4dfe4]': day.day === maxDay.day,
						 }"
				/>
				<div class="name text-sm opacity-30">
					{{ day.day }}
				</div>
			</div>
		</div>
		<hr class="my-5">
		<div class="content__footer flex justify-between">
			<div class="content__footer__left">
				<header class="content__footer__left__header text-sm opacity-30">
					Total this month
				</header>
				<div class="content__footer__left__value text-3xl font-semibold">
					${{ totalPrevMonth }}
				</div>
			</div>
			<div class="content__footer__right flex flex-col justify-end">
					<div class="content__footer__right__value text-right font-semibold">
						{{'???'}}%
					</div>
					<div class="content__footer__right__sign text-sm opacity-30">
						from last month
					</div>
			</div>
		</div>
	</div>
</div>
</template>
<script>
import initialData from '../public/intialData.json'
export default {
	name: 'App',
	props: {
		daysToShow: {
			type: Object,
			validator(value) {
				const map = ['mon', 'tue', 'wed', 'thu', 'fri', 'sat', 'sun']
				value.forEach(day => {
					if(map.includes(day.day)) {
						const idx = map.findIndex(dayToRemove => dayToRemove === day.day)
						map.splice(idx,1)
					}
				})
				return value.length === 7 && !map.length
			},
			default: initialData
		},
		userBalance: {
			type: Number,
			default: 999.99
		},
		totalPrevMonth: {
			type: Number,
			default: 111.11
		}
	},
	mounted(){
		this.days = this.daysToShow
		this.listHandler()
	},
	data(){
		return {
			days: []
		}
	},
	computed: {
		maxValue(){
			return Math.max(...this.days.map(day => day.amount))
		},
		maxDay(){
			return this.days.find(day => day.amount === this.maxValue)
		},
		totalWeek(){
			return this.days.reduce((sum, el) => sum + el.amount, 0)
		},
	},
	methods: {
		listHandler(){
			this.days.forEach(day => {
				day['day'] ??= 'null'
				day['amount'] ??= null
				Object.assign(day, {
					'heightBar': this.heightHandler(day.amount),
					'active': false
				})
			})
		},
		heightHandler(value){
			return value * 100 / this.maxValue
		},
	}
}
</script>
