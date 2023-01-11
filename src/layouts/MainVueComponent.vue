<script setup>
	import { store } from '../store.js';
	import Entreprise from '../components/Entreprise.vue';
	import WhoIs from '../components/WhoIs.vue';

	import {computed} from 'vue';

	defineProps({
		experiences: Object
	})


	const isExpVisible = true;

	function toggleNav(type) {
		// e.dataset.type
		if(type === 'exp') {
			console.log('exp !!! ', type)
			store.pageTypeVisible = true;

		} else if ( type === 'who') {
			console.log('who !!! ', type)
			store.pageTypeVisible = false;
		}
	}

</script>

<template>
	<div>
		<div class="nav-container">

			<nav>
				<ul>
					<li>
						<a href="#" title="Expériences" data-type="exp" @click="toggleNav('exp')">Expériences</a>
					</li>
					<li>
						<a href="#" title="Qui suis-je" data-type="who" @click="toggleNav('who')">Qui suis-je</a>
					</li>
				</ul>
			</nav>

		</div>
		<div class="main-container">


		
			<div v-if="store.pageTypeVisible">

				<transition name="exp">
					<Entreprise :experiences="experiences" />
				</transition>

			</div>

			<div v-else>

				<transition name="exp">
						<WhoIs />
				</transition>

			</div>

		</div>
	</div>

</template>

<style lang="scss" scoped>

* {
	margin: 0;
	padding: 0;
}



.nav-container {

	height: 50px;
	width: 20%;
	// border: 1px solid black;
	margin: auto auto;
	display: flex;
    justify-content: center;
	// position: absolute;

	nav {
		width: 100%;
		margin: auto 0;
	

		ul {
			display:flex;
			// justify-content: space-around;

			li { list-style: none;
				a {
					padding: 0px 20px;
					text-decoration: none;
					&:visited {
						color: inherit;
					}
				} 
			}
		}
	}
}

</style>

