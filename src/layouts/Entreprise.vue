<script setup>
	// import  { store }  from '../store'

	import {ref} from 'vue';
	import { useElementVisibility } from '@vueuse/core'
	import { watch } from '@vue/runtime-core';


	defineProps({
		experiences: Object
	})


	// const targetElement = ref(null); 
    // const targetIsVisible = useElementVisibility(targetElement);

	// watch(targetIsVisible, (newVal, oldVal) =>  {
	// 	console.log('target is visible  : ', newVal);
	// } ) 

	let isDetailsVisible = true;



</script>

<template>
	<div class="container">
		<div v-for="exp in experiences.experiences" :key="exp.id">
			<h1 class="titre">{{exp.name}}</h1>
			<section ref="targetElement" class="box" >
				<!-- <span></span> -->
				<span :style="{background: 
				'linear-gradient('+ exp.colors.deg + ', '+
				exp.colors.left + 
				', ' + 
				exp.colors.right +
				')'}"></span>
				
				<div class="content">
					<div class="exp-object">
						<div class="image">
							<a :href="exp.link" :class="exp.id" target="_blank" :title="exp.name"><img :src="exp.img" :alt="exp.name"></a>
						</div>
						<!-- <p class="date">
							<time :datetime="exp.date.from">{{exp.date.monthFrom}}</time>
							<span> à </span>
							<time :datetime="exp.date.to">{{exp.date.monthTo}} {{exp.date.year}}</time>
						</p> -->
					</div>

					<div class="exp-mission">
						<div class="marge-mission">
							<div class="description">
								<p v-html="exp.mission.description"></p>
							</div>
							<div class="env">
								<a v-for="env in exp.env" :key="env.id" class="stack" :href="env.link" target="_blank" rel="noopener noreferrer" :title="env.text + ' !'">

									{{env.text}}

								</a>
							</div>
						</div>
					</div>

					<div class="exp-details" v-if="isDetailsVisible">
						<div class="marge-mission">
							<ul>
								<li v-for="details in exp.details" :key="details.id">- {{ details }}</li>
							</ul>
						</div>
					</div>
				</div>
			</section>
		
			

		</div>
	</div>


	
</template>


<style lang="scss" scoped>

$primary: #333;
$blue: rgb(28, 90, 148);

$bgColor: var(--colors);

.box {
	&:hover {
		span {
			border-radius: 8px ;
			transform: skewX(0deg) scaleX(1.3);
		}
	}

	position: relative;
	height: 300px;
	display: flex;
	justify-content: center;
	align-items: center;
	transition: 0.5s;
	z-index: 1;
	will-change: transform; 
}



span {
	position: absolute;
	top: 0px;
	left: 6%;
    width: 49%;
	height: 300px;
	text-decoration: none;
	background: linear-gradient(315deg, #ffbc00, #ff0058);
	border-radius: 8px;
	transform: skewX(15deg);
	z-index: -10;
	transition: 0.5s;
}

.box .content {
	position: relative;
	width: 5000px;
	height: 254px;
	background: rgba(255, 255, 255, 0.05);
	backdrop-filter: blur(8px);
	box-shadow: 0 5px 15px rgba(0, 0, 0, 0.1);
	border-radius: 8px;
	z-index: 1;
	transform: 0.5s;
	color: #fff;
	display: flex;
	align-items: center;
}





@media screen and (max-width: 1000px) {
	#dark-light-container > div {
		width: 100%;
	}
}

	* { 
	font-family: 'Roboto', sans-serif;
	}

	$tablette: 1080px;
	$mobile: 470px;
	/* Expérience CONTAINER  */

	.marge-mission {
		display: flex;
		margin: 0 10px;
		flex-direction: column;
	}

	/* Expérience Object 30% */
	.titre {
		margin: 0 auto;
		color: $primary;
		letter-spacing: 2px;
		font-family: 'Sofia Sans Condensed', sans-serif;
	}
	.exp-object {
		display: flex;
		justify-content: space-between;
		flex-direction: column;
		width: 30%;


		.date {
			color: $primary;
		}
		.image  {
			margin: 0 auto;

			a img {
				margin: 0 auto;
				width: 200px;
			}
		} 
	}

	.exp-details {
		color:#0f0f10;
		width: 40%;
		font-size: 16px;
	}

	.exp-mission {
		width: 30%;
		color:#0f0f10e5;
		display: flex;
		justify-content: center;
		flex-direction: column;
	}

	.env {
		width: 100%;
		justify-content: space-evenly;
		display:flex;
	

		a {
			padding: 8px 11px;
			font-size: 13px;
			white-space: nowrap;
			transition: transform 0.3s;
			&:hover {
				transform: scale(1.1);
			}
		}
	}

	header {
		top: 0;
		width: 100%;	
		height: 350px;
		display: flex;
		align-items: center;
		color: #fff;
	}

	.fake-header {
		height: 50px;
	}

	ul li {
		list-style: none;
		font-size: 14px;
	}

	section {
		// border: solid 1px #333;
		width: 95%;
		max-width: 1800px;
		margin: 0 auto;
		height: 50vh;
		display: flex;
		justify-content: space-between;
		transition: all 0.75s;
		opacity:1;
		margin-bottom: 30px;

		
	}

	.judith {
		background-color:#0f0f10;
		padding: 19px 7px 7px 8px;
    	border-radius: 10px;
	}

	.bold-text {
		font-weight: bold;
	}

	 a {
		text-decoration: unset;
	
	}



	/* TABLETTE Media Query pour écran moins de 1080px */
	@media (max-width: $tablette) {
		section {
			flex-direction: column;
			height: fit-content;
		}

		.exp-object {
			width: 100%;
		}	
		.exp-mission {
			width: 100%;
		}	
		.exp-details {
			width: 100%;
		}

		.env {
			justify-content: space-evenly;

			a {
				margin: 5px 0;
			}
		}
	}
	/* Fin Media Query pour moins de 700px */

	/* MOBILE Media Query pour écran moins de 470px */
	@media (max-width: $mobile) {
		.env {
			flex-direction: column;
		}

	}
	/* Fin Media Query pour moins de 700px */


</style>

