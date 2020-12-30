<template>
	<div id="rules" class="view">
		<div class="view-container">
			<div class="stripe">
				<div id="rules-content" class="stripe-content normal-text">
					<div class="align-left">
						<h2>Szabályzat</h2>
					</div>
					<div class="align-left">
						<p>
							A játékosoknak együtt kell dolgozniuk, hogy megtalálják maguk között a 
							<strong>hamis művészt</strong>, míg ez a játékos megpróbálja elkerülni a lebukást.
						</p>
						<p>
							A játékosok minden körben látják a véletlenszerű kulcsszót és a hozzá tartozó kategóriát, pl.: <span>"Étel/Ital: Alma".</span>
						</p>
						<p>
							A hamis művész azonban <em>csak</em> a kategóriát látja, pl.: "Étel/Ital: ???".
						</p>
						<p>
							A játékosok felváltva rajzolnak a vászonra, egyszerre csak egy ecsetvonással. Miután mindenki kétszer sorra került, a játékosok szavaznak, hogy szerintük ki a hamis művész.
						</p>
						<p>
							A hamis művész nyer, ha nem ő kapja a többségi szavazatot.
						</p>
						<p>
							Ha el is kapják a hamis művészt, ő tippelhet egyszer a kulcsszóra.
							Ha eltalálja, <em>nyer!</em>
						</p>
					</div>
					<div class="align-right">
						<button class="btn secondary" @click="back()">OK</button>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
import Store from './state';
import VIEW from './view';
export default {
	name: 'RulesView',
	methods: {
		back() {
			Store.setView(Store.state.previousView);
		},
	},
};
</script>
