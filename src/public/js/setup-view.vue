<template>
	<div id="room-setup" class="view">
		<div class="view-container">
			<Confirmation
				id="confirm-leave"
				confirmText="Kilépés"
				v-show="leaveConfirmationDialogVisible"
				@close="leaveConfirmationDialogVisible = false"
				@confirm="leave"
			>
				<h2>Kilépés?</h2>
				<div class="normal-text">
					<p>Biztos, hogy kilépsz a játékból?</p>
				</div>
			</Confirmation>
			<Confirmation
				id="confirm-start"
				confirmText="Indítás"
				v-show="startConfirmationDialogVisible"
				@close="startConfirmationDialogVisible = false"
				@confirm="start"
			>
				<h2>Új játék?</h2>
				<div class="normal-text">
					<p>Amíg a játék tart, nem tudnak csatlakozni új játékosok.</p>
					<p>
						Játékosok hozzáadásához később válaszd a "Kilépés a létrehozás menübe"
						lehetőséget.
					</p>
				</div>
			</Confirmation>

			<div class="stripe flex-center align-center game-code">
				<div class="stripe-content">
					<div id="setup-header">Szoba kód:</div>
					<h1>{{ roomCode }}</h1>
				</div>
			</div>

			<div class="stripe flex-center align-center users">
				<div class="stripe-content">
					<div id="setup-header">Játékosok:</div>
					<ul class="users">
						<li v-for="username in usernames" :key="'0' + username">{{ username }}</li>
					</ul>
				</div>
			</div>

			<div class="stripe flex-center align-center actions">
				<div class="stripe-content">
					<button class="btn primary big" @click="startConfirmationDialogVisible = true">
						Játék indítása
					</button>
					<div style="clear: both" />
					<button class="btn tertiary" @click="leaveConfirmationDialogVisible = true">
						Kilépés
					</button>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Store from './state';
import VIEW from './view';
import Confirmation from './confirmation';
export default {
	name: 'SetupView',
	components: {
		Confirmation,
	},
	props: {
		roomCode: {
			type: String,
		},
		usernames: {
			type: Array,
		},
	},
	data() {
		return {
			leaveConfirmationDialogVisible: false,
			startConfirmationDialogVisible: false,
		};
	},
	watch: {},
	methods: {
		start() {
			Store.submitStartGame();
		},
		leave() {
			Store.setView(VIEW.HOME);
			Store.submitLeaveGame();
		},
	},
};
</script>
