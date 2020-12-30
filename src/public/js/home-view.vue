<template>
	<div id="home" class="view">
		<div class="view-container">
			<div id="title-banner" class="stripe align-center">
				<div class="stripe-content">
					<h1 class="title">Hamis Művész Online</h1>
				</div>
			</div>
			<div class="stripe flex-center">
				<home-menu></home-menu>
			</div>
		</div>
	</div>
</template>
<script>
import HomeMenu from './home-menu';
export default {
	name: 'HomeView',
	components: {
		HomeMenu,
	},
};
</script>
