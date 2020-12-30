<template>
	<div id="home-menu" class="flex-center">
		<div id="first-prompt-menu" class="menu" v-show="tab === 'main'">
			<button id="goto-create-menu" class="btn big primary" @click="setTab('create')">
				Új játék
			</button>
			<div style="clear: both"></div>
			<button id="goto-join-menu" class="btn big primary" @click="setTab('join')">
				Csatlakozás
			</button>
			<div style="clear: both"></div>
			<button class="btn big secondary" @click="gotoRules()">Szabályzat</button>
		</div>

		<div id="create-game-menu" class="menu" v-show="tab === 'create'">
			<div class="warning" v-show="store.createWarning !== undefined">
				<p>{{ store.createWarning }}</p>
			</div>
			<form id="create-game-form" @submit.prevent="createGame">
				<input
					type="text"
					id="create-username-input"
					class="username-input"
					placeholder="Felhasználónév"
					required
					autocomplete="off"
					v-model="store.username"
					maxlength="15"
				/>
				<div style="clear: both"></div>
				<div class="form-actions">
					<button
						type="button"
						id="create-game-back-btn"
						class="btn tertiary"
						@click="setTab('main')"
					>
						Vissza
					</button>
					<button
						type="submit"
						id="create-game-btn"
						class="btn primary"
						value=""
						:disabled="!Boolean(store.username)"
					>
						Létrehozás
					</button>
				</div>
			</form>
		</div>

		<div id="join-game-menu" class="menu" v-show="tab === 'join'">
			<div class="warning" v-show="store.joinWarning !== undefined">
				<p>{{ store.joinWarning }}</p>
			</div>
			<form id="join-game-form" @submit.prevent="joinGame">
				<input
					type="text"
					id="join-username-input"
					class="username-input"
					placeholder="Felhasználónév"
					required
					autocomplete="off"
					v-model="store.username"
					maxlength="15"
				/>
				<div style="clear: both"></div>
				<input
					type="tel"
					id="join-code"
					placeholder="Szoba kód"
					required
					autocomplete="off"
					v-model="store.roomCode"
				/>
				<div style="clear: both"></div>
				<div class="form-actions">
					<button
						type="button"
						id="join-game-back-btn"
						class="btn tertiary"
						@click="setTab('main')"
					>
						Vissza
					</button>
					<button
						type="submit"
						id="join-game-btn"
						class="btn primary"
						:disabled="!Boolean(store.username && store.roomCode)"
					>
						Csatlakozás
					</button>
				</div>
			</form>
		</div>
	</div>
</template>

<script>
import Store from './state';
import VIEW from './view';

export default {
	name: 'home-menu',
	components: {},
	data() {
		return {
			store: Store.state,
			tab: 'main',
		};
	},
	methods: {
		setTab(value) {
			this.tab = value;
		},
		gotoRules() {
			Store.setView(VIEW.RULES);
		},
		gotoFaq() {
			Store.setView(VIEW.FAQ);
		},
		createGame() {
			Store.submitCreateGame(Store.state.username);
		},
		joinGame() {
			Store.submitJoinGame(Store.state.roomCode, Store.state.username);
		},
	},
	watch: {
		'store.username'(val) {
			Store.setUsername(val);
		},
	},
};
</script>
