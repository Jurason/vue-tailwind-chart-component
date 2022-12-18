<template>
<div class="container">
	<div class="header">
		<div class="header__content">
			<div class="header__content__title">
				My balance
			</div>
			<div class="header__content__balance">
				{{  }}
			</div>
		</div>
		<div class="header__toggle">

		</div>
	</div>
	<div class="content">
		<header class="content__header">
			Spending - Last 7 days
		</header>
		<div class="content__graph">
			<div class="content__graph__item">
				<div class="value hidden">{{}}</div>
				<div class="graph-value"></div>
				<div class="name">{{}}</div>
			</div>
		</div>
		<hr>
		<div class="content__footer">
			<div class="content__footer__left">
				<header class="content__footer__left__header">
					Total this month
				</header>
				<div class="content__footer__left__value">
					{{}}
				</div>
			</div>
			<div class="content__footer__right">
					<div class="content__footer__right__value">
						{{}}
					</div>
					<div class="content__footer__right__sign">
						from last month
					</div>
			</div>
		</div>
	</div>
</div>
	<div class="design">
		<img src="./expenses-chart-component-main/design/active-states.jpg" alt="">
	</div>
</template>
<script>

</script>
<style>

</style>
