<template>
	<dialog-component id="vote-dialog">
		<div v-show="!isTurnEnd">
			<h2>Szavazz, hogy ki a Fake Artist:</h2>
		</div>
		<div v-show="isTurnEnd">
			<h2>Eredény:</h2>
		</div>
		<div v-show="!isTurnEnd">
			<PlayerListForVote
				:users="users"
				v-on:changeVote="setVotedUsername"
				:votedUsername="votedUsername"
			/>
		</div>
		<div v-show="isTurnEnd">
			<PlayerListVotes :users="users" />
		</div>

		<template #actions>
			<div>
				<button
					v-show="!isTurnEnd"
					class="btn secondary"
					:disabled="!isValidUsername"
					@click="submit()"
				>
					Szavazás
				</button>
				<button v-show="isTurnEnd" class="btn secondary" @click="$emit('close')">
					Bezárás
				</button>
			</div>
		</template>
	</dialog-component>
</template>

<script>
import Store from './state';
import VIEW from './view';
import DialogComponent from './dialog';
import PlayerListForVote from './player-list-for-vote';
import PlayerListVotes from './player-list-votes';
export default {
	name: 'VoteDialog',
	components: {
		DialogComponent,
		PlayerListForVote,
		PlayerListVotes,
	},
	props: {
		users: {
			type: Array,
		},
		isTurnEnd: {
			type: Boolean,
		},
	},
	data() {
		return {
			votedUsername: null,
		};
	},
	computed: {
		isValidUsername() {
			return Store.state.gameState.findUser(this.votedUsername);
		},
	},
	methods: {
		submit(username) {
			this.$emit('vote', this.votedUsername);
			this.votedUsername = 'Válassz játékost';
			this.$emit('close');
		},
		setVotedUsername(username) {
			this.votedUsername = username;
		},
	},
};
</script>
