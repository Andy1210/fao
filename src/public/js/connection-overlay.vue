<template>
	<div id="conn-overlay" class="flex-center" v-show="!connected">
		<div id="reconnecting-message">{{ message }}</div>
	</div>
</template>

<script>
import Store from './state';
import CONNECTION_STATE from './connection-state';

export default {
	name: `ConnectionOverlay`,
	components: {},
	props: {
		gameConnection: {
			type: String,
			required: true,
		},
	},
	computed: {
		connected() {
			return this.gameConnection === CONNECTION_STATE.CONNECT;
		},
		message() {
			if (Store.state.joinWarning) {
				return 'Hiba a csatlakozáskor: ' + Store.state.joinWarning;
			}
			return 'Csatlakozás...';
		},
	},
};
</script>
